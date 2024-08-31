
# BUILDING ROCK PAPER SCISSORS GAME

# IMPORTING REQUIRED MODULES
from tkinter import *
from PIL import Image, ImageTk
import random


# Creating a window
root = Tk()
root.geometry('790x400')
root.title("ROCK PAPER SCISSORS GAME ")
root.configure(background="Dark violet")

# ADDING IMAGES TO WINDOW

# FOR USER
rock_img = ImageTk.PhotoImage(Image.open("20595-7-dwayne-johnson-picture-thumb.png"))
paper_img = ImageTk.PhotoImage(Image.open("—Pngtree—roll paper cartoon stationery_4681546.png"))
scissors_img = ImageTk.PhotoImage(Image.open("pngwing.com.png"))


# FOR COMPUTER
rock_img_comp = ImageTk.PhotoImage(Image.open("20595-7-dwayne-johnson-picture-thumb.png"))
paper_img_comp = ImageTk.PhotoImage(Image.open("—Pngtree—roll paper cartoon stationery_4681546.png"))
scissors_img_comp = ImageTk.PhotoImage(Image.open("pngwing.com.png"))

# POSITIONING IMAGE
user_label = Label(root, image=scissors_img, bg="Dark violet", relief=RAISED, borderwidth=5)
comp_label = Label(root, image=scissors_img_comp, bg="Dark violet", relief=RAISED, borderwidth=5)
user_label.grid(row=1, column=4)
comp_label.grid(row=1, column=0)


# INSERTING SCORES
user_score = Label(root, text=0, font=100, bg="Dark violet", fg="black")
computer_score = Label(root, text=0, font=100, bg="Dark violet", fg="black")
user_score.grid(row=1, column=3)
computer_score.grid(row=1, column=1)


# SIGNAL
user_signal = Label(root, font=50, text="User", bg="grey25", fg="white", relief=SUNKEN, borderwidth=8)
comp_signal = Label(root, font=50, text="Computer", bg="grey25", fg="white", relief=SUNKEN, borderwidth=8)
user_signal.grid(row=0, column=3)
comp_signal.grid(row=0, column=1)

# MESSAGE BOX
msg = Label(root, font=50, bg="Dark violet", fg="black", text="You lose !")
msg.grid(row=3, column=2)


# UPDATING MESSAGES
def update_messages(x):
    msg["text"] = x


# UPDATING SCORES
def update_scores():
    score = int(user_score["text"])
    score += 1
    user_score['text'] = str(score)


def update_comp_score():
    score = int(computer_score["text"])
    score += 1
    computer_score['text'] = str(score)


def check_winner(choice, comp_choice):
    if choice == comp_choice:
        update_messages("It's tie !!")
    elif choice == "ROCK":
        if comp_choice == "PAPER":
            update_messages("You Lose !")
            update_comp_score()
        else:
            update_messages("You Win")
            update_scores()
    elif choice == "PAPER":
        if comp_choice == "SCISSORS":
            update_messages("You Lose!")
            update_comp_score()
        else:
            update_messages("You Win")
            update_scores()
    elif choice == "ROCK":
        if comp_choice == " SCISSORS ":
            update_messages("You lose !")
            update_comp_score()
        else:
            update_messages("You Win")
            update_scores()

    else:
        pass


comp_choice_list = ["ROCK", "PAPER", "SCISSORS"]


def choices(choice):
    # COMPUTER CHOICES
    comp_choice = comp_choice_list[random.randint(0, 2)]

    if comp_choice == "ROCK":
        comp_label.configure(image=rock_img)
    elif comp_choice == "PAPER":
        comp_label.configure(image=paper_img)
    else:
        comp_label.configure(image=scissors_img)

    # USER CHOICES

    if choice == "ROCK":
        user_label.configure(image=rock_img)
    elif choice == "PAPER":
        user_label.configure(image=paper_img)
    else:
        user_label.configure(image=scissors_img)
    check_winner(choice, comp_choice)


# BUTTON FOR CHOICES
rock = (Button(root, width=20, height=2, text="ROCK",
               bg="grey25", fg="white", command=lambda: choices("ROCK"), relief=SUNKEN, borderwidth=5)
        .grid(row=2, column=1))
paper = (Button(root, width=20, height=2, text="PAPER",
                bg="grey25", fg="white", command=lambda: choices("PAPER"), relief=SUNKEN, borderwidth=5)
         .grid(row=2, column=2))
scissors = (Button(root, width=20, height=2, text="SCISSORS",
                   bg="grey25", fg="white", command=lambda: choices("SCISSORS"), relief=SUNKEN, borderwidth=5)
            .grid(row=2, column=3))


root.mainloop()
