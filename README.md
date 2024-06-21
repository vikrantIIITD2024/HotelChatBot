# HotelChatBot

HotelChatBot is an AI-driven chatbot designed to assist with various hotel-related inquiries, such as booking rooms, canceling reservations, requesting special offers, and more. The chatbot leverages natural language processing (NLP) and machine learning techniques to understand and respond to user queries accurately. This project is implemented using Python and integrates the Ollama LLModel and Google Translate API for enhanced language processing capabilities.

## Features

- **Room Booking**: Users can book rooms for specified dates and number of guests.
- **Reservation Cancellation**: Allows users to cancel existing bookings.
- **Special Offers**: Provides information on any special deals or discounts available.
- **Local Attractions**: Gives recommendations on nearby attractions.
- **Complaint Resolution**: Handles user complaints and provides resolutions.
- **Availability Check**: Informs users about room availability.
- **Room Rate Inquiry**: Provides details on room rates.
- **Booking Modification**: Allows users to modify existing bookings.

## Installation

To run the HotelChatBot, you'll need to install the required dependencies. You can install them using pip:

```bash
pip install googletrans==4.0.0-rc1 transformers
```

## Usage

The chatbot script includes functions for various operations. Below is a brief overview of the main components:

### Fibonacci Sequence

A simple function to generate a Fibonacci sequence:

```python
def fibonacci(n):
    res = [0, 1]
    for i in range(2, n + 1):
        res.append(res[i - 1] + res[i - 2])
    return res

n = int(input())
fibonacci(n)
```

### Language Translation

Utilizes Google Translate API for translating text:

```python
from googletrans import Translator

def hitoen(sentence):
    translator = Translator()
    out = translator.translate(sentence, dest='en')
    return out.text
```

### Annotations Generation

Uses the Ollama LLModel to generate annotations for user queries:

```python
import ollama

def generateAnnotations(line):
    data = {
        'classes': ["book_room", "cancel_booking", "request_special_offer", "ask_about_local_attractions", "resolve_complaint", "check_availability", "inquire_room_rate", "modify_booking"],
        'annotations': []
    }
    
    ents = {'entities': []}
    response = ollama.chat(model='llama2', messages=[
        {
            'role': 'user',
            'content': f'In the following: {line} what is the user asking for out of {data["classes"]}'
        },
    ])
    print(response['message']['content'])

if __name__ == "__main__":
    filename = "I want to book a room for two adults."
    generateAnnotations(filename)
```

### Running the ChatBot

To start the chatbot, run the script and interact with the provided prompts. The chatbot will handle conversations, translate messages as needed, and generate appropriate responses.

```bash
python hotelchatbot.py
```

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request for any improvements or new features.

## License

This project is licensed under the MIT License.
