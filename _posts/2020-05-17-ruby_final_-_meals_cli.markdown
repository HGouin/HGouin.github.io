---
layout: post
title:      "Ruby Final - Meals CLI"
date:       2020-05-17 20:36:29 +0000
permalink:  ruby_final_-_meals_cli
---

My meals CLI project was a great way for me to apply all of the skills I have learned over the past few months. There were plenty of ups and downs going through this, but in the end I feel very confident and happy with what I was able to put together while juggling everything else in life.

For this project I decided to create a Meals CLI because cooking is one of my passions and I thought it would be fun to create something that ties into what I really enjoy.

Here is a flow chart of what it is like to go through the app I created:

[Meals CLI Flowchart](https://drive.google.com/file/d/1eftBKlVjU3K0XuL3PhR8jTJ62e_Yt4tH/view?usp=sharing)


As  you snake through you will see that meal, ingredient, and instruction objects were created, that the user is able to input a main ingredient to get a list of meals for that ingredient, that they have the option to view all the ingredients for that meal as well as go step by step through the instructions. The user is asked for input, the app goes out to gather that information from the website, and then retrieves the information for the user (creating the objects).

I was able to have some fun with this app and add features that we did not learn about in the course. Google is a wonderful tool! I had fun adding `STDIN.getch` so that the user is able to press a single character to navigate between the instructions, or to go back to list of meals for that main ingredient they entered. Adding that feature let me to tap into a more creative side. 

A question that came up during a one-on-one was why I was using Meals.clear. I thought my original explanation was not conveyed with confidence or a true understanding as to why I chose to do that in my app. Here is a better explanation:
I decided to have a Meals.clear function because I do not need to keep track of every meal object. I am reaching out to the API every time to get the latest results and eventually I would like to add pagination to go through more than just the top ten results. Since I am doing the fetch every time the main ingredient is changed, there is no reason to hold onto the meals for old main ingredients.

A struggle I ran into was the user navigation through the app. The nested CLI levels were new and challenging. As you can see there are multiple while loops for different levels of the user's place in the app. There is the highest level which is where you can see a list of meals for the ingredient you have entered, choose to change the ingredient, or exit the app. The next level after you have chosen a meal allows you to either print the ingredients for the meal or enter the final level which allows you to navigate through the instructions. At this final level, you can see the current step and, if applicable, the ingredients necessary for that step.

```
while input != "exit"
            if input == 'list'
                print_meals(Meal.all)
                ##go ahead and list my dinners with this ingredient again
            elsif input.to_i > 0 && input.to_i <= Meal.all.length 
                meal = Meal.all[input.to_i - 1]
                Api.getIngredients(meal)
                Api.getAnalyzedInstructions(meal)#user picks a dinner, go ahead and get the detail for that dinner
                while input != 'b'
                    puts "  "
                    puts "Recipe: #{meal.name}"
                    prompt_user_recipe
                    input = STDIN.getch
                    
                    if input == 'b'
                        break
                    elsif input == 'i'
                        meal.print_ingredients
                    elsif input == 't'
                        step = 0
                        if meal.instructions.length == 0
                            puts "No instructions found for that meal"
                        else 
                            meal.print_instruction(step)
                            while input != 'b'
                                prompt_user_instructions
                                input = STDIN.getch
                                if input == 'b'
                                    input = ''
                                    break
                                elsif input == 'n'
                                    step -= 1
                                    step = 0 if step < 0
                                elsif input == 'm'
                                    step +=1
                                    if step == meal.instructions.length
                                    step = meal.instructions.length - 1
                                    puts "Already on the last step"
                                    end
                                end
                                meal.print_instruction(step)
                            end
                        end
                    end
                end
            elsif input == "ingredient"
                #elsif #user picks another dinner
                puts "Enter a main ingredient to see meals made with that ingredient"
                puts "  "
                Meal.clear
                @main_ingredient = gets.strip.downcase
                Api.get_meals(@main_ingredient)
                input = 'list'
                next
            else 
                puts "I do not understand, please try again"
            end
            if input == 'b'
                input = "list"
                next
            end
            prompt_user
            input = gets.strip.downcase
        end
```


Overall, this project was a great introduction and I learned so much! 
![](https://media3.giphy.com/media/9rhPKWpmTf3BesSxou/giphy.gif)

You can check out my full project [here](https://github.com/HGouin/Ruby-Final)
