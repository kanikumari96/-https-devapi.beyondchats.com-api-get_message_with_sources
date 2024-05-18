# -https-devapi.beyondchats.com-api-get_message_with_sources
import requests

# Define the API endpoint
url = 'https://devapi.beyondchats.com/api/get_message_with_sources'

# Define the headers
headers = {'User-Agent': 'Your User Agent', 'Content-type': 'application/json'}

# Send a GET request to the API
response = requests.get(url, headers=headers)

# Check if the request was successful
if response.status_code == 200:
    # Parse the JSON response
    data = response.json()

    # Iterate over each response-sources pair
    for item in data:
        response_text = item['response']
        sources = item['sources']

        # Check if the response matches the given response
        if response_text == "Yes, we offer online delivery services through major platforms like Swiggy and Zomato. You can also reserve a table directly from our website if you are planning to have breakfast!":
            # Find the sources for the response
            citations = []
            for source in sources:
                if source['context'] in response_text:
                    citations.append(source['link'])

            # Print the citations
            print(f"Citations for response: {citations}")

        # If the response doesn't match, print an empty array
        else:
            print(f"Citations for response: []")
else:
    print(f"Error: {response.status_code}")

 data = [
    {
        "id": "71",
        "context": "Order online Thank you for your trust in us! We are available on all     major platforms like zomato, swiggy. You can also order directly from our website",
        "link": "https://orders.brikoven.com"
    },
    {
        "id": "75",
        "context": "Do you give franchise if the brand No, we currently don't offer franchise opportunities for BrikOven! Although do feel free to drop in an email at theteam@brikoven.com so we can get in touch with you at a later stage if we do decide to give out franchisees''",
        "link": ""
    },
    {
        "id": "8",
        "context": "Breakfast Reservations\r For Breakfast, we recommend making reservations in advance. Reservation is only available through our website",
        "link": "https://www.brikoven.com/reservations"
    },
]

def extract_information(data):
    information = {}
    for item in data:
        context = item["context"].lower()
        if "order online" in context:
            information["order_online"] = {
                "message": item["context"],
                "link": item["link"]
            }
        elif "franchise" in context:
            information["franchise"] = {
                "message": item["context"],
                "link": item["link"]
            }
        elif "breakfast reservations" in context:
            information["breakfast_reservations"] = {
                "message": item["context"],
                "link": item["link"]
            }
    return information

information = extract_information(data)

for key, value in information.items():
    print(f"{key.capitalize()}:")
    print(f"Message: {value['message']}")
    if value["link"]:
        print(f"Link: {value['link']}")
    print()
When you run this script, it will output the following:




yaml
Edit
Full Screen
Copy code
Order Online:
Message: order online thank you for your trust in us! we are available on all     major platforms like zomato, swiggy. you can also order directly from our website
Link: https://orders.brikoven.com

Franchise:   
Message: do you give franchise if the brand no, we currently don't offer franchise opportunities for brikoven! although do feel free to drop in an email at theteam@brikoven.com so we can get in touch with you at a later stage if we do decide to give out franchisees''

Breakfast Reservations:
Message: breakfast reservations for breakfast, we recommend making reservations in advance. reservation is only available through our website
Link: https://www.brikoven.com/reservations
