#git-practice
age = int(input("Enter your age:"))

if age < 0 or age > 120:
    print("Invalid age")
elif 0 <= age <= 12:
    print("Child")
elif 13 <= age <= 19:
    print("Teenager")
elif 20 <= age <= 64:
    print("Adult")
else:
    print("Senior")




weight = float(input("Enter your weight (kg): "))
height = float(input("Enter your height (m): "))
bmi = weight / (height ** 2)
print(f"Your BMI is {bmi:.2f}")
if bmi < 18.5: 
    print ("Underweight")
elif 18.5 <= bmi <= 24.9:
    print ("Normal")
elif 25 <= bmi <= 29.9: 
    print ("Overweight")
else:
    print ("Obese")




score = int (input("Enter your score"))

print (f"Your score is {score:.1f}%")
if 90 <= score <= 100:
    print ("A")
elif 80 <= score <= 89:
    print ("B")
elif 70 <= score <= 79:
    print ("C")
elif 60 <= score <= 69:
    print ("D")
else:
    print ("F")




Celcius = float (input("Enter temperaure in Celcius"))
Fahrenheit = (Celcius * 9 / 5) + 32
print (f"Celcius is {Celcius:.1f} and Fahrenheit is {Fahrenheit:.1f}")
if Celcius < 0:
    print ("Freezing!")
elif 0 <= Celcius <= 15:
    print ("Cold")
elif 16 <= Celcius <= 25:
    print ("Mild")
elif 26 <= Celcius <= 35:
    print ("Warm")
else:
    print ("Hot")




speed = float (input("Enter current speed"))
print (f"Speed:{speed:.1f}")
if speed < 20:
    print ("Too slow, speed up!")
elif 20 <= speed <= 60:
    print ("Safe speed")
elif 61 <= speed <= 100:
    print ("Caution: Getting fast")
else:
    print ("Warning: Over-speeding!")




total_bill = float(input("Enter your total bill amount"))
service = (input("Please, rate the service. Enter one of the following: bad, okay, good, excellent"))
if service == "bad":
    tip_percentage = 0.00
elif service == "okay":
    tip_percentage = 0.10
elif service == "good":
    tip_percentage = 0.15
elif service == "excellent":
    tip_percentage = 0.20
else:
    print ("Invalid input. Please, enter one of the options mentioned")
tip_amount = total_bill * tip_percentage
print (f"Tip amount:{tip_amount:.2f}CAD")
total_to_pay = total_bill + (total_bill * tip_percentage)
print (f"Total to pay:{total_to_pay:.2f}CAD")



weight = float(input("Enter weight in kg"))
time = float(input("Enter duration in minutes"))
type = input("Please, enter the exercise type: walking, running or cycling").lower()
if type == "walking":
    met = 3.5
elif type == "running":
    met = 7.0
elif type == "cycling":
    met = 6.8
else:
    print ("Invalid input.")
    exit()
calories = met * weight * (time / 60)
print (f"Calories burned: {calories:.2f}")
if calories < 200:
    print ("Light activity")
elif 200 <= calories <= 400:
    print ("Moderate workout")
else:
    print ("Intense session")




x = float (input("Enter x value."))
y = float (input("Enter y value."))
result = x + y
print (f"The sum of {x:.2f} and {y:.2f} is {result:.2f}")


name = input ("Enter item name")
price = float(input("Enter item price"))
print (f"Item: {name}")
print (f"Item price: {price:.2f}")


book = []
book1 = input ("Enter your favourite book 1")
book.append(book1)
book2 = input ("Enter your favourite book 2")
book.append(book2)
book3 = input ("Enter your favourite book 3")
book.append(book3)
book4 = input ("Enter your favourite book 4")
book.append(book4)
book5 = input ("Enter your favourite book 5")
book.append(book5)
book.sort()
print (book)
# book.remove(book5)
# print ("Updated book list", book)
#books.sort(reverse=True) 
#print("Books in reverse alphabetical order:", books)
#sorted_books = sorted(books, reverse=True)
print("Books in reverse alphabetical order:", sorted_books)



names = [input(f"Enter name {i + 1}: ") for i in range (5)]
name_updated = [name.strip().title() for name in names]
for name in name_updated:
    print(f"Welcome, {name}!")



places = [input(f"Enter your favorite travelling place {i + 1}: ").strip().title() for i in range (5)]
if "Japan" in place:
    print ("Japan is an amazing destination!")
else:
    print ("You might want to add Japan to your list!")
places.sort()
for place in places:
    print (f"Your favorite place {place}!")

numbers = [int(input(f"Enter your favorite number {i + 1}: ")) for i in range (5)]
for number in numbers: 
    if number %2 != 0:
        print (f"{number} is odd")
    else:
        print(f"{number} is even")
numbers.sort(reverse = True)
for i, number in enumerate(numbers, 1) :
    print (f"Your favorite number {i} is: {number}")




n = int(input())
for i in range (n):
    print (i **2)


number = int(input("Enter a number"))
if number / 2 > 0:
    print("It's an even number")
else:
    print("It's an odd number")





try:
    num = int(input("Enter numerator"))
    den = int(input("Enter denominator"))
    result = (num / den)
    print("Result is:", result)
except ValueError: 
    print("Invalid input! Please enter a number.")
except ZeroDivisionError:
    print("You cant devide by 0")




# Changes statuses of orders in a list to new statuses.

from pythoniser import change_statuses, orders_from_list, STATUSES, cancel_order, \
    stage_order, get_order
import time

# SUPPORT: fill in

env = "wings-prod"
status_to = "served"
orders = orders_from_list("orders_sheet.csv")


# Script itself:
for order in orders:
    order_json = get_order(env, order)
    try:
        current_status = order_json["response"]["status"]
    except (TypeError, KeyError) as e:
        print(f"Could not get {order} status")
        current_status = None

    # some orders are stuck under "shipped" which is no longer used
    # a workaround is to assume these orders are "staged"
    # this will apply all the statuses that go after "shipped" ...
    # ... starting from "ready"
    if current_status == "shipped":
        current_status = "staged"


    # current_status will be None for some errors, 404 for instance

    # get_order_status will return None for sCDX-CD25972458ome errors, 404 for instance

    # so we only proceed if there is some non-empty status like "picked"
    if current_status:
        if current_status == "draft" and status_to not in ["canceled", "cancelled"]:
            print(f"❄️ Can't push draft {order} because it's not split yet")
        elif status_to in ["canceled", "cancelled"] and current_status != "cancelled":
            cancel_order(env, order)

        elif current_status != "cancelled":
            # these clients require the staging location present
            if env.startswith("alpha") or env.startswith("abs"):
                staging = get_order(env, order)["response"]["stage-location"]
                if staging is None:
                    stage_order(env, order)

            index_status_from = STATUSES.index(current_status)
            index_status_to = STATUSES.index(status_to)
            statuses_todo = STATUSES[index_status_from+1:index_status_to+1]
            change_statuses([order], statuses_todo, env)

        else:
            continue

# delay ensures that database has time to accept our write operations ...
# ... before we check for updated order statuses
print("🥭 🐀 🦅 Verifying status transition ...")
time.sleep(5)

for order in orders:
    try:
        new_status = get_order(env, order)["response"]["status"]
    except (TypeError, KeyError) as e:
        new_status = None

    if new_status in ["canceled", "cancelled"]:
        continue
    elif new_status != status_to:
        print(f"❄️ ❄️: {order} is stuck under {new_status}, and not moved to {status_to}")






countries = {
    "Ukraine": "Kyiv",
    "Canada": "Ottawa",
    "France": "Paris",
    "Japan": "Tokyo"
}


regions = {
    "Ukraine": "Europe",
    "Canada": "North America",
    "France": "Europe",
    "Japan": "Asia"
}

while True:
    try:
        country = input("Enter a country: ").strip()
        capital = countries[country]
        region = regions[country]  # 🆕 Retrieve the region using the country as the key
        print(f"The capital of {country} is: {capital}")
        print(f"Region: {region}")
        break
    except KeyError:
        print("Sorry, that country is not in the list.")



countries = {
    "Ukraine": "Kyiv",
    "Canada": "Ottawa",
    "France": "Paris",
    "Japan": "Tokyo"
}

regions = {
    "Ukraine": "Europe",
    "Canada": "North America",
    "France": "Europe",
    "Japan": "Asia"
}

while True:
    country = input("Enter a country: ").strip()
    capital = countries.get(country)
    region = regions.get(country)

    if capital and region:
        print(f"The capital of {country} is: {capital}")
        print(f"Region: {region}")
        break
    else:
        print("Sorry, that country is not in the list.")



#This is my first Git + GitHub test!

#one more update