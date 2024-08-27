# README

## Overview

This project provides a simple web service using FastAPI that allows for real-time communication with a language model via WebSockets. The service listens for incoming WebSocket connections, receives user messages, processes them using a model from the `ollama` library, and sends back the generated responses.

## Features

- **WebSocket API**: The application supports bi-directional communication using WebSockets. This allows for real-time messaging between the client and server.
- **Language Model Integration**: The service integrates with the `ollama` library to generate responses using a specified language model.
- **Asynchronous Operation**: The service is built on Python's `asyncio` framework, enabling non-blocking communication and efficient handling of multiple connections.

## Prerequisites

Before running the application, ensure you have the following installed:

- Python 3.8+
- FastAPI
- Uvicorn (for serving the FastAPI app)
- `ollama` library (Ensure you have access to the `ollama` library and the appropriate model files)

## Installation

1. **Clone the repository**:

   ```bash
   git clone https://your-repo-url.git
   cd your-repo-directory
   ```

2. **Install the required dependencies**:

   ```bash
   pip install fastapi uvicorn ollama
   ```

3. **Ensure the `ollama` library is configured properly**:
   - Follow the `ollama` library's documentation for setup and model configuration.

## Running the Application

To start the FastAPI application, run the following command:

```bash
uvicorn app:app --host 192.168.0.37 --port 9999
```

This will start the server on the specified host (`192.168.0.37`) and port (`9999`).

## WebSocket Endpoint

### URL

- `ws://192.168.0.37:9999/ws`

### Usage

1. **Connect to the WebSocket**:

   Establish a connection to the WebSocket endpoint using a client that supports WebSocket communication (e.g., a web browser or a WebSocket client).

2. **Send a message**:

   Send a text message through the WebSocket. The message will be processed by the `ollama` model, and a response will be generated.

3. **Receive a response**:

   The server will send back a JSON response containing the model's reply. The response format is:

   ```json
   {
       "status": 204,
       "response": "Generated response from the model"
   }
   ```

4. **Handle disconnection**:

   If the client disconnects, the server will log the event.

## Code Overview

### `websocket_endpoint(websocket: WebSocket)`

- This is the main WebSocket handler function. It accepts incoming WebSocket connections and listens for text messages. Upon receiving a message, it invokes `get_response` to generate a response using the `ollama` model.

### `get_response(message: str)`

- This function interfaces with the `ollama` library, sending the user's message to the model and returning the generated response.

### `if __name__ == "__main__":`

- This block starts the FastAPI application using Uvicorn when the script is executed directly.

## Customization

- **Model Selection**: The `get_response` function uses the `llama3` model by default. You can change the model by modifying the `model` parameter in the `ollama.chat` call.
- **Host and Port**: Adjust the host and port settings in the Uvicorn command or modify the parameters in the `uvicorn.run` function in the script.

## Troubleshooting

- **WebSocket Connection Issues**: Ensure the client is correctly configured to communicate over WebSocket with the server.
- **Model Errors**: Verify that the `ollama` library and the specified model are correctly installed and configured.

## License

This project is licensed under the MIT License. See the `LICENSE` file for more information.

## Acknowledgements

- [FastAPI](https://fastapi.tiangolo.com/)
- [Uvicorn](https://www.uvicorn.org/)
- [Ollama](https://ollama.com/) for the language model integration.
