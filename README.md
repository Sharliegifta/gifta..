Problem 1: Real-Time Weather Monitoring System

Scenario:

You are developing a real-time weather monitoring system for a weather forecasting company. The system needs to fetch and display weather data for a specified location.

Tasks:

1.	Model the data flow for fetching weather information from an external API and displaying it to the user.

2.	Implement a Python application that integrates with a weather API (e.g., OpenWeatherMap) to fetch real-time weather data.

3.	Display the current weather information, including temperature, weather conditions, humidity, and wind speed.

4.	Allow users to input the location (city name or coordinates) and display the corresponding weather data.

Deliverables:

•	Data flow diagram illustrating the interaction between the application and the API.

•	Pseudocode and implementation of the weather monitoring system.

•	Documentation of the API integration and the methods used to fetch and display weather data.

•	Explanation of any assumptions made and potential improvements.

 

Approach:

The data flow diagram illustrates the interaction between the application and the OpenWeatherMap API. The application receives user input for the location, fetches the weather data from the API, and displays the current weather information to the user.

                                      +---------------+

                                      |  User Input  |

                                      +---------------+

                                             |

                                             |  Location

                                             v

                                      +---------------+

                                      |  Fetch Weather  |

                                      |  Data from API  |

                                      +---------------+

                                             |

                                             |  Weather Data

                                             v

                                      +---------------+

                                      |  Display Weather  |

                                      |  Information to  |

                                      |  User            |                                +---------------+

Pseudocode:

# Function to fetch weather data from OpenWeatherMap API

def fetch_weather_data(location):

    api_key = "YOUR_OPENWEATHERMAP_API_KEY"

    api_url = f"http://api.openweathermap.org/data/2.5/weather?q={location}&appid={api_key}"

    response = requests.get(api_url)

    if response.status_code == 200:

        data = response.json()

        return data

    else:

        return None



# Function to display weather data to the user

def display_weather_data(data):

    if data:

        print(f"Current Weather in {data['name']}:")

        print(f"Temperature: {data['main']['temp']}°C")

        print(f"Weather Conditions: {data['weather'][0]['description']}")

        print(f"Humidity: {data['main']['humidity']}%")

        print(f"Wind Speed: {data['wind']['speed']} m/s")

    else:

        print("Error fetching weather data.")



# Main function to handle user input and display weather data

def main():

    location = input("Enter a city name or coordinates: ")

    data = fetch_weather_data(location)

    display_weather_data(data)



# Run the main function

if __name__ == "__main__":

    main()

Detailed explanation of the actual code:

1.	fetch_weather_data: This function takes a location as input and fetches the weather data from the OpenWeatherMap API. It uses the requests library to send a GET request to the API with the location and API key. If the response is successful (200 status code), it parses the JSON response and returns the data. Otherwise, it returns None.

2.	display_weather_data: This function takes the weather data as input and displays the current weather information to the user. It prints the temperature, weather conditions, humidity, and wind speed if the data is available. If there is an error fetching the data, it prints an error message.

3.	main: This function handles user input and calls the fetch_weather_data and display_weather_data functions. It prompts the user to enter a location, fetches the weather data, and then displays the data to the user.

Assumptions made (if any):

1.	The user will always enter a valid location.

2.	The OpenWeatherMap API will always return data in the expected format.

Limitations:

1.	The application does not handle errors in the API response.

2.	It does not validate user input for location.

3.	It does not provide any additional features like historical weather data or weather forecasts.

Code:

import http.client

import json



def get_weather(api_key, location):

    conn = http.client.HTTPConnection("api.openweathermap.org")

    conn.request("GET", f"/data/2.5/weather?q={location}&appid={api_key}&units=metric")

    response = conn.getresponse()

    if response.status == 200:

        data = json.loads(response.read().decode("utf-8"))

        return {

            "temperature": data["main"]["temp"],

            "weather_condition": data["weather"][0]["description"],

            "humidity": data["main"]["humidity"],

            "wind_speed": data["wind"]["speed"]

        }

    else:

        return {"error": "Failed to retrieve weather data"}



def display_weather(weather_data):

    print("Current Weather Data:")

    print(f"Temperature: {weather_data['temperature']}°C")

    print(f"Weather Condition: {weather_data['weather_condition']}")

    print(f"Humidity: {weather_data['humidity']}%")

    print(f"Wind Speed: {weather_data['wind_speed']} m/s")



def main():

    api_key = input("Enter your OpenWeatherMap API key: ")

    location = input("Enter the location (city name): ")

    weather_data = get_weather(api_key, location)

    if "error" in weather_data:

        print(weather_data["error"])

    else:

        display_weather(weather_data)



if __name__ == "__main__":

    main()



Sample Output / Screen Shots 

 

 

Problem 2: Inventory Management System Optimization

Scenario:

You have been hired by a retail company to optimize their inventory management system. The company wants to minimize stockouts and overstock situations while maximizing inventory turnover and profitability.

Tasks:

1.	Model the inventory system: Define the structure of the inventory system, including products, warehouses, and current stock levels.

2.	Implement an inventory tracking application: Develop a Python application that tracks inventory levels in real-time and alerts when stock levels fall below a certain threshold.

3.	Optimize inventory ordering: Implement algorithms to calculate optimal reorder points and quantities based on historical sales data, lead times, and demand forecasts.

4.	Generate reports: Provide reports on inventory turnover rates, stockout occurrences, and cost implications of overstock situations.

5.	User interaction: Allow users to input product IDs or names to view current stock levels, reorder recommendations, and historical data.

Deliverables:

•	Data Flow Diagram: Illustrate how data flows within the inventory management system, from input (e.g., sales data, inventory adjustments) to output (e.g., reorder alerts, reports).

•	Pseudocode and Implementation: Provide pseudocode and actual code demonstrating how inventory levels are tracked, reorder points are calculated, and reports are generated.

•	Documentation: Explain the algorithms used for reorder optimization, how historical data influences decisions, and any assumptions made (e.g., constant lead times).

•	User Interface: Develop a user-friendly interface for accessing inventory information, viewing reports, and receiving alerts.

•	Assumptions and Improvements: Discuss assumptions about demand patterns, supplier reliability, and potential improvements for the inventory management system's efficiency and accuracy.

 

Approach:

+---------------+     +-------------------+

|   User Input  |     |   Inventory API    |

+---------------+     +-------------------+

       |                      |

       |  User requests       |

       |  inventory updates    |  Inventory data

       |  and reorder options   |

       v                      v

+---------------+     +-------------------+

| Inventory App |     |     Database       |

+---------------+     +-------------------+

       |                      |

       |  Fetch inventory data |  Store inventory data

       |  and reorder info      |

       v                      v

+---------------+     +-------------------+

|  User Output  |     |   Notification     |

+---------------+     +-------------------+

1.	User Input: Users input product IDs, request inventory updates, and reorder options.

2.	Inventory API: Provides real-time inventory data and alerts.

3.	Inventory App: Central application that processes user requests and interacts with the database.

4.	Database: Stores current stock levels, product details, and transaction history.

5.	User Output: Displays current stock levels, reorder recommendations, and historical data to users.

6.	Notification: Sends alerts for low stock levels or other important inventory updates.

Pseudocode:

# Define the inventory system structure

define Product, Warehouse, and InventoryLevel classes



# Implement the inventory tracking application

class InventoryTrackingApp:

    def __init__(self, products, warehouses):

        self.products = products

        self.warehouses = warehouses

        self.inventory_levels = self.initialize_inventory_levels()



    def initialize_inventory_levels(self):

        # Initialize inventory levels based on the provided data

        inventory_levels = []

        for product in self.products:

            for warehouse in self.warehouses:

                inventory_level = InventoryLevel(product, warehouse, initial_stock)

                inventory_levels.append(inventory_level)

        return inventory_levels



    def track_inventory(self):

        # Monitor inventory levels and send alerts when stock falls below threshold

        for inventory_level in self.inventory_levels:

            if inventory_level.current_stock < inventory_level.reorder_point:

                send_alert(inventory_level)



# Optimize inventory ordering

def calculate_reorder_point(product, warehouse, historical_sales, lead_time):

    # Calculate the optimal reorder point based on historical sales and lead time

    safety_stock = calculate_safety_stock(historical_sales, lead_time)

    reorder_point = safety_stock + (average_daily_sales * lead_time)

    return reorder_point



def calculate_reorder_quantity(product, warehouse, historical_sales, lead_time, reorder_point):

    # Calculate the optimal reorder quantity based on historical sales, lead time, and reorder point

    economic_order_quantity = calculate_economic_order_quantity(historical_sales, holding_cost, ordering_cost)

    reorder_quantity = max(economic_order_quantity, product.minimum_order_quantity)

    return reorder_quantity



# Generate reports

def generate_inventory_turnover_report(inventory_levels):

    # Calculate and report on inventory turnover rates

    pass



def generate_stockout_report(inventory_levels):

    # Report on stockout occurrences and their cost implications

    pass



def generate_overstock_report(inventory_levels):

    # Report on overstock situations and their cost implications

    pass



# User interaction

class InventoryManagementUI:

    def __init__(self, inventory_tracking_app):

        self.inventory_tracking_app = inventory_tracking_app



    def display_inventory_information(self, product_id):

        # Allow users to view current stock levels, reorder recommendations, and historical data

        pass



Detailed explanation of the actual code:

1.	Defining the Inventory System Structure: I will create classes for Product, Warehouse, and InventoryLevel to represent the components of the inventory system. These classes will store relevant information about each entity, such as product details, warehouse locations, and current stock levels.

2.	Implementing the Inventory Tracking Application: The InventoryTrackingApp class will be responsible for initializing the inventory levels, tracking the current stock, and sending alerts when stock falls below a certain threshold. The track_inventory() method will continuously monitor the inventory levels and trigger alerts as needed.

3.	Optimizing Inventory Ordering: The calculate_reorder_point() and calculate_reorder_quantity() functions will implement algorithms to determine the optimal reorder point and quantity for each product in each warehouse. These calculations will be based on historical sales data, lead times, and other relevant factors.

4.	Generating Reports: The generate_inventory_turnover_report(), generate_stockout_report(), and generate_overstock_report() functions will generate the required reports on inventory performance, stockouts, and overstock situations, respectively.

5.	User Interaction: The InventoryManagementUI class will provide a user-friendly interface for accessing inventory information, viewing reports, and receiving alerts. Users will be able to input product IDs or names to retrieve the desired information.



Assumptions made (:if any)

1.	The company has a well-defined product catalog and warehouse locations.

2.	Historical sales data and lead times are available for the inventory optimization algorithms.

3.	The company has defined thresholds for reorder points and minimum order quantities.

4.	The cost of holding inventory and placing orders are known.



Limitations:

1.	The current implementation assumes constant lead times, which may not always be the case in real-world scenarios.

2.	The demand forecasting algorithms are not included in the pseudocode, as they can be complex and require more detailed analysis of the company's sales patterns.

3.	The user interface is only briefly mentioned, and a more comprehensive design would be required for a production-ready system.



Code:

class Product:

    def _init_(self, product_id, name, current_stock, reorder_point, reorder_quantity):

        self.product_id = product_id

        self.name = name

        self.current_stock = current_stock

        self.reorder_point = reorder_point

        self.reorder_quantity = reorder_quantity



class Warehouse:

    def _init_(self, warehouse_id, location):

        self.warehouse_id = warehouse_id

        self.location = location

        self.products = []



def track_inventory(products):

    for product in products:

        if product.current_stock < product.reorder_point:

            print(f"Alert: {product.name} is below the reorder point. Current stock: {product.current_stock}")

            recommend_reorder(product)



def recommend_reorder(product):

    new_stock = product.current_stock + product.reorder_quantity

    print(f"Recommended reorder for {product.name}: {product.reorder_quantity} units. New stock level: {new_stock}")



def calculate_reorder_point(historical_sales, lead_time, desired_service_level):

    # Implement algorithms to calculate the optimal reorder point

    # based on historical sales data, lead time, and desired service level

    pass



def calculate_reorder_quantity(historical_sales, lead_time, holding_cost, ordering_cost):

    # Implement algorithms to calculate the optimal reorder quantity

    # based on historical sales data, lead time, holding cost, and ordering cost

    pass



def generate_inventory_report(products):

    # Generate reports on inventory turnover rates, stockout occurrences, and cost implications of overstock situations

    pass



def user_interface():

    # Define sample products and warehouses

    product1 = Product(1, "Product A", 50, 20, 30)

    product2 = Product(2, "Product B", 15, 10, 25)

    warehouse1 = Warehouse(1, "Warehouse A")

    warehouse1.products = [product1, product2]



    while True:

        user_input = input("Enter a product ID or name (or 'exit' to quit): ")

        if user_input.lower() == "exit":

            break



        # Look up the product and display current stock, reorder recommendations, and historical data

        for product in warehouse1.products:

            if str(product.product_id) == user_input or product.name.lower() == user_input.lower():

                print(f"Product: {product.name}")

                print(f"Current Stock: {product.current_stock}")

                recommend_reorder(product)

                # Display historical data

                break

        else:

            print("Product not found.")



# Test the application

user_interface()



Sample Output / Screen Shots 

 



 

Problem 3: Real-Time Traffic Monitoring System

Scenario:

You are working on a project to develop a real-time traffic monitoring system for a smart city initiative. The system should provide real-time traffic updates and suggest alternative routes.

Tasks:

1.	Model the data flow for fetching real-time traffic information from an external API and displaying it to the user.

2.	Implement a Python application that integrates with a traffic monitoring API (e.g., Google Maps Traffic API) to fetch real-time traffic data.

3.	Display current traffic conditions, estimated travel time, and any incidents or delays.

4.	Allow users to input a starting point and destination to receive traffic updates and alternative routes.

Deliverables:

•	Data flow diagram illustrating the interaction between the application and the API.

•	Pseudocode and implementation of the traffic monitoring system.

•	Documentation of the API integration and the methods used to fetch and display traffic data.

•	Explanation of any assumptions made and potential improvements.

 

Approach:

1. Data Flow Diagram

Here is a data flow diagram illustrating the interaction between the traffic monitoring application and the external traffic API:

text

+---------------+     +---------------+

|   User Input  |     |   Traffic API |

+---------------+     +---------------+

       |                      |

       |  User requests       |

       |  traffic updates     |  Traffic data

       |  and route           |

       v                      v

+---------------+     +---------------+

|  Traffic App  |     |   Database    |

+---------------+     +---------------+

       |                      |

       |  Fetch traffic data  |  Store traffic data

       |  and route options   |

       v                      v

+---------------+     +---------------+

|   User Output |     |   Notification|

+---------------+     +---------------+



The key steps in the data flow are:

•	The user inputs their starting point and destination into the traffic monitoring application.

•	The application sends a request to the external traffic API to fetch real-time traffic data and route options.

•	The traffic API provides the requested data, which the application stores in a local database.

•	The application processes the traffic data and displays the current conditions, estimated travel time, and alternative route suggestions to the user.

•	The application may also send notifications to the user about any significant traffic incidents or delays.





Pseudocode:

text

import requests

def get_traffic_data(start, end):

    # Call the traffic API to fetch real-time data

    api_key = "your_api_key"

    url = f"https://maps.googleapis.com/maps/api/directions/json?origin={start}&destination={end}&key={api_key}"

    response = requests.get(url)

    data = response.json()



    # Extract relevant traffic information

    current_traffic = data["routes"][0]["legs"][0]["duration_in_traffic"]["text"]

    estimated_travel_time = data["routes"][0]["legs"][0]["duration"]["text"]

    alternative_route
