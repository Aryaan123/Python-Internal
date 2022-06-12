# Python-Internal
#imports the built in random and time module
import random
import time

#list of all the questions for the quiz and sorted by difficulty
beginner_questions = [
     "Tokyo is the capital of Japan. True or False?",
     "Beijing is the capital of South Korea. True or False?",
     "Australia is one of the 7 continents of the world. True or False?",
     "Capital city of Canada is Toronto. True or False?",
     "Russia is located in Europe. True or False?",
     "Tokyo is the most populated city in the world. True or False?",
     "New Zealand has no states. True or False?",
     "Canada is located in the northern hemisphere. True or False?",
     "South Africa has 2 capital cities. True or False?",
     "Antartica isn't a continent. True or False?",
]

intermediate_questions = [
    "How many countries are there in the world?\nA: 195\nB: 215\nC: 192\nD: 189",
    "What is the capital city of India?\nA: Mumbai\nB: New Dehli\nC: Dehli\nD: Kolkata",
    "What is the largest desert in the world?\nA: Antarctic Desert\nB: Sahara Desert\nC: Artic Desert\nD: Arabian Desert",
    "Turkey is a country in Asia. True or False?",
    "What is the capital city of Vietnam?\nA: Hanoi\nB: Manila\nC: Kuala Lumpur\nD: Phuket",
    "What is the largest lake in the world?\nA: Lake Victoria\nB: Lake Superior\nC: Caspian Sea\nD: Lake Huron",
    "What is the most densely populated country?\nA: South Korea\nB: Bangaladesh\nC: India\nD: United Kingdom",
    "Which country shares a borders with North Korea?\nA: South Korea\nB: Japan\nC: Mongolia\nD: Hong Kong",
    "Mexico City is the Capital of Mexico. True or False?",
    "Which of these are not a city in Spain?\nA: Barcelona\nB: Porto\nC: Bilbao\nD: Valencia"
]

advanced_questions = [
    "What is the short form of the state of Arizona",
    "What place is known as the largest micro-continent?", 
    "How many time zones does Australia have?",
    "What is the capital city of Estonia?",
    "What country is in between Spain and France?",
    "What is the capital city of Uzbekistan?",
    "Which country has the oldest flag?",
    "Switzerland has four national languages, English being one of them. True or False",
    "What is the capital city of Scotland?",
    "What is the 7th most populated country in the world?"
]

#list of all the answers for the questions and sorted by difficulty
beginner_answers = [
    "true", "false", "false", "false", "true", "true", "false", "true", "true", "false",
]

intermediate_answers = [
    "a", "b", "a", "true", "a", "a", "b", "b", "true", "b",
]

advanced_answers = [
    "az", "madagascar", "3", "tallinn", "andorra", "tashkent", "denmark", "false", "edinburgh", "nigeria",
]

#list of responses to user answers
correct_reply = [
    "That's the correct answer", "Nice you got it right!", "correct!", "That is the right answer!",
    "You're correct!", "You're right!", "That's right. Get the next one as well!"
]

incorrect_reply = [
    "Better luck next time", "Bad luck but that's the wrong answer", "incorrect!",
    "Sorry but that is the wrong answer", "Unfortunately that is wrong", "You are wrong!"
]

#Makes the user pick and sets a difficulty for the quiz
def mode():
    while True:  
        global questions        #allows questions to be used outside of function
        global answers      #allows answers to be used outside of function
        difficulty = input("      Please choose a difficulty\n      - beginner\n      - intermediate\n      - advanced\n{}: ". format(name))
        difficulty = difficulty.strip().lower()      
        if difficulty == "beginner":
            questions = beginner_questions
            answers = beginner_answers
            break
        elif difficulty == "intermediate":
            questions = intermediate_questions
            answers = intermediate_answers
            break
        elif difficulty == "advanced":
            questions = advanced_questions
            answers = advanced_answers
            break
        else:
            print("Please choose a valid option")

#goes through all the questions in the relevant difficulty list
def quiz():
    i = 0
    global score
    score = 0
    for question in questions:
        #makes user choose valid answer if question is multichoice or true or false
        while True:
            print("\nQuestion {}" .format(i + 1))
            user_answer = input("{}\n{}: " .format(question, name))
            user_answer = user_answer.lower().strip()
            if answers[i] == "true" or answers[i] == "false":
                if user_answer == "true" or user_answer == "false":
                    break
                else:
                    print("Host: Please answer with True or False.")
                    time.sleep(1)
            elif  answers[i] == "a" or answers[i] == "b" or answers[i] == "c" or answers[i] == "d":
                if user_answer == "a" or user_answer == "b" or user_answer == "c" or user_answer == "d":
                    break
                else:
                    print("Please answer with A,B,C or D.")
                    time.sleep(1)
            else:
                break
        if user_answer == answers[i]:
            print("{}" .format(random.choice(correct_reply)))
            time.sleep(1)     #adds a delay
            i += 1      #adds one to i so that it goes onto the next question
            score += 1
        else:
            print("{}" .format(random.choice(incorrect_reply)))
            time.sleep(1)     #adds a delay
            i += 1      #adds one to i so that it goes onto the next question
   
#tells and comments on the user's final score
def total_score():
    print("\nHost: Your final score was", score, "out of", len(questions))
    if score in range(0, 5):
        time.sleep(1)     #adds a delay
        print ("     You can do better!")
    elif score == 5:
        time.sleep(1)
        print("      You got half right!")
    elif score in range(6, 10):
        time.sleep(1)     #adds a delay
        print ("      That's a really good score!")
    else:
        time.sleep(1)     #adds a delay
        print ("      That is a perfect score!")

def name():
    #global name allows the variable name to be used outside the function
    global name
    while True:
        name = input("What is your name? ")
        name = name.strip().title()
        if name.isalpha():
            break
        else:
            print("Please only enter name in letters")

    
    
       
#sets retry to yes so that the user goes through the quiz at least once before they can quit
retry = "yes"

#asking the user for their year level
def recommend():
    while True:
        age = int(input("What is your year level?"))
        if age in range(9,11):
            print("I recommend you play the beginner level")
            break
        elif age == 11:
            print("I recommend you play the intermediate level")
            break
        elif age in range(12,14):
            print("I recommend you play the advanced level")
            break
        else:
            print("Please enter a year level between 9-13")
    

#welcomes the user to the quiz and calls the quiz function. After it prints a score and response on the score
print("Welcome, This quiz has 3 difficulties with 10 questions each!")
print("      They are all about geography so let's see how much you know about the world!")
time.sleep(2.5)
name()
print("Hello {} it is an honour to meet you!" .format(name))
recommend()
time.sleep(1)       #adds a delay
print("      Before we get started here are the instructions:")
print("      The beginner level is only true or false questions, the intermediate questions")
print("      are multi choice questions and finally the advanced questions are questions that") 
print("      you will have to answer on your own. Be careful because for the advanced questions")


time.sleep(2)     #adds a delay
while retry == "yes":
    print("Good luck!")
    mode()
    quiz()
    total_score()
    while True:
        retry = input("      Would you like to try the quiz again? yes or no\n{}: " .format(name))
        retry = retry.strip().lower()
        if retry == "yes" or retry =="no":
            time.sleep(1.5)     #adds a delay
            break
        else:
            print("Please answer with yes or no")
print("Thanks for playing!")




