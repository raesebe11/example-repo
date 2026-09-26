#compound interest formula A=P(1+r)^t  (annual compounding)
#simple interest formula   A=P(1+rt)
#bond repayment formula    repayment = (r/12 * P) / (1 - (1 + r/12)^(-months))
#where:
# A = the future value of the investment
# P = the principal investment amount / present value of the bond
# r = the annual interest rate (in decimal)
# t = the number of years the money is invested / repaid

import math

# ---------------------------------------------------------
# Main menu: choose investment or bond calculation.
# Case-insensitive, keeps asking until a valid choice is made.
# ---------------------------------------------------------
while True:
    calc_type = input("Would you like to calculate 'investment' or 'bond'? ").strip().lower()
    if calc_type in ("investment", "bond"):
        break
    print("Invalid choice. Please type 'investment' or 'bond'.\n")


if calc_type == "investment":
    # ---------------------------------------------------------
    # Sub-menu: simple or compound interest
    # Case-insensitive, keeps asking until a valid choice is made.
    while True:
        interest_type = input("Would you like 'simple' or 'compound' interest? ").strip().lower()
        if interest_type in ("simple", "compound"):
            break
        print("Invalid choice. Please type 'simple' or 'compound'.\n")

    principal = float(input("Enter the principal investment amount ($): "))
    rate = float(input("Enter the annual interest rate (as a %): ")) / 100
    time = float(input("Enter the number of years the money is invested: "))

    if interest_type == "simple":
        # Simple interest: A = P(1 + rt)
        A = principal * (1 + rate * time)
    else:
        # Compound interest (annual compounding): A = P(1 + r)^t
        A = principal * math.pow((1 + rate), time)

    interest_earned = A - principal

    print(f"\nThe future value of the investment is ${A:.2f}.")

    #give feedback to the user based on the interest rate
    if interest_earned > principal * 0.1:
        print("The interest rate is quite low. You might want to consider other investment options.")
    elif interest_earned < principal * 0.1:
        print("The interest rate is quite high. You are earning a good return on your investment.")
    else:
        print("The interest rate is moderate. You are earning a fair return on your investment.")

    #show the user how much interest they earned
    print("\n--- Interest Earned ---")
    print("interest type: ", interest_type)
    print("final amount: {:.2f}".format(A))
    print("interest earned: {:.2f}".format(interest_earned))


else:  # calc_type == "bond"
    # Bond repayment calculator
    
    present_value = float(input("Enter the present value of the house ($): "))
    rate = float(input("Enter the annual interest rate (as a %): ")) / 100
    years = float(input("Enter the number of years to repay the bond: "))

    months = years * 12
    monthly_rate = rate / 12

    # Standard bond repayment formula
    repayment = (monthly_rate * present_value) / (1 - math.pow((1 + monthly_rate), -months))

    print(f"\nYour monthly bond repayment is ${repayment:.2f}.")# example-repo
