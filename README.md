# Textgame
Python Text Game
#######################################################################
# Dong Hoon Lee - Constructing Staee_1 and calling it to start the game
########################################################################

"""

DocString: 
    
    A) Introduction:
    California driver's license application game
    
    Round 1: (Y/N) Requirement - Age 
    Round 2: (Multiple - Nested) Finding fast way in the website
    Round 3: (Multiple - conditional - Not allowed - Payment option 
    Round 4: (Guess) Lottery for fast lane chance - 3 chances

    Game Idea from California DMV <https://www.dmv.ca.gov/portal/dmv>
    More information https://www.aceable.com/blog/how-to-get-your-license-when-youre-new-to-california/

    B) Known Bugs and/or Errors:
    Error happened when user did not input any value to random function.
    
"""

# Package import
from sys import exit

def game_start():
    global name  
    # Minimize global variable to maintain consistency

# Starter 
    name = input("What is your last name?  ")
    print(f"Welcome {name}!")
    input('<Press ENTER key to start game "CA DMV Application">\n')

    print(f"""
      Hi {name}!
      This is a new guide program about DMV.
      You can learn the fastest way to apply for a California Driver License.
      Also, try the DMV's new offering of lottery for your convenience.
      """)
    
    step_1()

#Step_1 - Conditional (Yes,no?)

def step_1(): 
    print("Are you over 16 years old?")
    age_stat = input("Yes or No? ")

    # Age check
    if 'n' in age_stat.lower(): 
        print("Bye! You are not allowed to apply for it")
        exit()
    
    elif 'y' in age_stat.lower(): 
        print("\nNow You are ready to take this tour.")
        print(f"""
          First, you need to go to DMV website.
          Let's FInd out what is the fast menu to process.      
          """)     
        step_2()
    else:
        print("Invalid entry. Please try again.\n")
        step_1()

#Step_2 - Conditional - Nested - Best vs Second best

def step_2():
    print("Now you're in DMV website! It does not look kind.\n")
    input('<Press any key to continue>\n')
    print(
"""
Select the fast action menu to visit DMV.
Press 1 to [Online Services)]
Press 2 to [Appointment]
Press 3 to [Real ID]
""") 
    
    select = input("> ")
    
    # Start of conditional
    if select == '1':
        print("Possible. But you have to choose one more. \n")
        # This is the second best since it does not allow appointment
        print( 
"""
What's the next choice in the [Online Services)]?
1) Driver License and Certification Card
2) DMV Office Visit
        
""")
        
        select = input("> ")
        
        # Start of nested conditional
        if select == '1':
            print("That's not a good idea. Try again")
            step_2
          
        elif select =='2':
            print("That's it. Now you can book a date")
            print("Remember! [Appointment] is the best access")
            input('<Press any key to continue>\n')
        
        # End of nested conditional
                
    elif select == '2':
        print(
"""
Good job. Now you can make the visit appointment fast. 
""")
            
    elif select == '3':
        print("Oh sorry. Maybe you will swim in the menu for a while. \n")
        print("We can meet together next time. Bye! \n")
        fail()
        
    else:
        print(f"Invalid entry. Please try again at the website.{name}\n")
        input('<Press any key to continue>\n')
        step_2
        
    step_3()

#Step_3 - Conditional (Yes,no?)

def step_3():
            
    print(
"""     
Now you are preparing the fee before going to the DMV.   
Which of the following is allowed for the payment at the DMV?
(You don't have cash, check, money order)
 A. Debit Card
 B. Credit Card
""")
        
    select = input("Your choice is >>> ")
    
    if select.upper() == 'A':
        print("Great! Now You can apply to fast track lottery." )
        
    elif select.upper() == 'B': 
        print("Oh sorry. You should go back home and come later with debit card")
        fail()
        
    else:
        print(f"Invalid entry. Please try again.{name} \n")
        step_3()    
            
    step_4()

#Step_1 - Lottery (while loop with nested conditional)   

def step_4(): 
       
    import random

    print(
"""
DMV is offering a new fast lane services by lottery.
If you win, you will be served without any waiting.
You have 3 chances and choose a number between 1 and 5.
If you run out of chances, you should start the game again
""")

    number = random.randint(1,5)
    bet = 3

    bet = int(bet) # Not necessay, but training purpose
    
    #Start of while loop
    while bet > 0:
        choice = int(input('\n Your choice is (1-5)?\n> '))

        # Best choice so that user can get an exclusive right 
        if choice == number:
            print('\nYou made it!. You also save your valuable time!')
            print('\nCongratulations for your journey to DMV')
            break         
        
        # Remaing try until chance goes to 0
        elif choice != number:
            bet -= 1
            
            # Nested conditional up to three times trial
            if bet > 0:
                print(f"\nOh Sorry You have {bet} remaining.")
            
            elif bet == 0:
                print(f"\nYou are out of guesses. The number was {number}")
                fail()
            
            else:
                print(f"\nWrong. Please try again.")
                input("<Press enter to continue>\n")
                step_4()
            
        else:
            print(f"\nError. Please try again. Type number 1-5")
            input("<Press enter to continue>\n")
            step_4()
            
# Fail function  

def fail():
    print(f"\nYou lose it. Anyway you did a good job {name}. See you next time.\n")
    input("<Press enter to end the game>\n")
    exit()
    
game_start()
