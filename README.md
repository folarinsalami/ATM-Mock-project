# ATM MOCK PROJECT
# Project for Bank of Africa Automated Teller Machine will have the following inbuilt #functionalities
# Register function will have the following parameters
# - First name, last name, password, e-mail
# - Generate user account number
# Login function will have the following parameters 
# - Account number and password
# Bank Operation function comes last
# Initializing system
import random
import validation 
import database
from database import getpass

def init():
  print("Welcome to Bank of Savana Automated Teller Machine e-transaction platform")
  have_account = int(input(" Do you have an existing bank account with Bank of Savana? : 1 (Yes) 2 (No) \n"))
  if have_account ==1:
    login()
  elif have_account ==2:
   register()
  else:
    print("The option you have selected is not valid, please try again")
    init()
def login():
  print("Login")
  
  account_number= input("Please enter your account number \n")
  is_valid_account_number = validation.account_number_validation(account_number)
  if is_valid_account_number:
    password = getpass("What is your password\n")
    user = database.authenticated_user(account_number, password);
    if user:
      bank_operation(user)
    print("Invalid account or password")
    login()
  else: 
    print("Account Number Invalid: Check that you have up to 10 digits and only as integers ")
  init()
def register():
  print("***** Register ******")
  first_name= input("Please enter your first name\n")
  last_name= input("Please enter your  your last name")
  email = input( "Please enter your e-mail address")
  password= getpass("Please create a password for yourself\n")
  account_number = generation_account_number()
  is_user_created = database.create(account_number, first_name, last_name, email, password)
  if is_user_created:
    print("Congratulations your account has been set up")
    print("== === ========")

    login()
  else:
    print("An error has occured during your registration process, Kindly go through registration process and try again")
    register()
def bank_operation(user):
  print("Welcome %s %s " % (user[0], user[1]))
  selected_option = int(input("What would you like to do? (1) deposit (2) withdraw (3) Logout (4) Exit \n" ))

  if selected_option == 1:
    deposit_operation()
  elif selected_option ==2:
    withdrawal_operation()
  elif selected_option==3:
    logout()
  elif selected_option == 4:
    exit()
  else:
    print("You have selected an invalid option")
    bank_operation(user)
def withdrawal_operation():
  print("withdrawal")

  # Under this Fund withdrawal Opearation we will do do the following - 
  # Get the current balance
  # Get amount to withdrawal
  # Check if current balance is greater than  withdrawal balance
  # Subtract money withdrawn from current account balance
def deposit_operation():
  print("Deposit Operations")
  # Get current balance
  # Get amount to deposit
  # Add deposited anount to current account balance
  # Display current balance
def generation_account_number():
  return random.randrange(1111111111, 9999999999)
def set_current_balance(user_details, balance):
  user_details[4]= balance
def logout():
  login()
init()
 
