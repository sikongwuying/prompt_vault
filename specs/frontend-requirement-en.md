resource: https://catalog.us-east-1.prod.workshops.aws/workshops/41e422c0-0580-4443-9dc9-0bb5f2e36bc5/en-US/lab-3-aidlc-implement/lab-3-2-frontend


# Streamlit Weather Agent Chat Application Development Requirements

## Project Overview

Build a Streamlit chat application as a frontend interface for an already deployed Weather Agent. The agent is deployed and accessible via API calls.

## Core Functional Requirements

### 1. API Integration

```python
import requests
import json

# Call payload (adjust according to your agent API format)
def call_weather_agent(user_message: str):
    payload = {
        "message": user_message,
        "user_id": "streamlit_user"  # Optional user identification
    }
    
    headers = {
        "Content-Type": "application/json",
        "Authorization": f"Bearer {API_KEY}"  # Adjust according to your authentication method
    }
    
    response = requests.post(
        API_ENDPOINT,
        json=payload,
        headers=headers
    )
    
    return response.json()
```

### 2. User Interface

```python
# Use Streamlit native Markdown rendering support for weather information formatting
def render_chat_message(role: str, content: str, timestamp: str = None):
    # Render message header
    st.markdown(f"**{'You' if role == 'user' else '🧠 Weather Assistant'}**")

    # Render message content (automatically supports Markdown)
    st.markdown(content)
```

**UI Component Requirements:**

- Use `st.chat_message()` to create chat interface
- Distinguish visual styles between user messages and agent responses
- Real-time loading indicator (`st.spinner()`)
- Sidebar displaying connection status and configuration information

### 3. Session Management

```python
# Avoid Streamlit state conflicts
def process_user_input(user_input: str):
    try:
        # Processing logic...
        pass
    finally:
        # Clear loading state
        self.state_manager.set_loading_state(False)
        # ✅ Important: Force UI update
        st.rerun()
```

### Error Handling

- Handle authentication failures
- API connection issues
- Agent unavailability
- Network timeouts and other service errors
- Display specific error messages and troubleshooting suggestions

### Response Format Handling

Expected agent response format:

```json
{
  "response": "🌤️ **Weather Overview: Sunny, Few Clouds**\n- **Temperature: 32.1°C**...",
  "timestamp": "2025-08-29T02:11:14.883028",
  "status": "success"
}
```

**✅ Important:** Response content contains Markdown formatting and needs to be properly rendered using `st.markdown()`.

## UI/UX Design Requirements

### Main Interface

- Page title: "🧠 Weather Agent - Intelligent Weather Assistant"
- Chat input box at the bottom with send button
- Scrollable chat history area
- **✅ Markdown rendering support**, especially for weather information formatting (bold, emojis, etc.)

**Important** Please utilize the Figma MCP tool to reference the following Figma design for frontend interface planning:
[Chat AI Design](https://www.figma.com/design/3ODWNPDmpXVnQvoNbAkTrG/ChatGPT-v4.5--Chat-AI----AI-Chatbot--Community-?node-id=1-1702&t=UiAJkuv6H6Tw7qk6-4)

### Sidebar Information

- Connection status indicator (green=normal, red=error)
- Last update time
- Configuration check status
- Clear conversation button

### Status Display

- Loading: "Retrieving weather information..."
- Success: Display API call status
- Error: Detailed error messages and suggested solutions

## Example Conversation Flow

1. **User Input:** "How's the weather in Taipei today?"
2. **Loading State:** Display spinner and "Querying Taipei weather..."
3. **API Call:** Use the above payload format
4. **Response Processing:** Parse JSON response and extract weather information
5. **Display Results:** Use `st.markdown()` to display formatted weather information

## Test Scenarios

- Basic weather query: "What's the weather like in Tokyo right now?"
- Multi-city comparison: "Which city is better for travel, Taipei or Tokyo?"
- Clothing advice: "I'm going to Sydney tomorrow, what should I wear?"
- Error handling: Test network issues, authentication failures, etc.

## Success Criteria

✅ Successfully connect to the deployed Weather Agent  
✅ Correctly display weather information and clothing recommendations  
✅ Good user experience and error handling  
✅ Responsive design suitable for different screen sizes  
✅ Proper Markdown rendering and UI state management

**Note:** Please create a complete, simple, and usable Streamlit application according to the above specifications, ensuring the use of the exact configuration values provided and implementing all necessary functionality.