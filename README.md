Fork of https://github.com/lpigeon/ros-mcp-server

Functionality redesigned for Brewie robot specifics

# Brewie under LLM Control

Transform your robot into an understandable and accessible tool with MCP server!

## Key Updates

### Updated ROS Connection Method
Fixed errors with connection method calls through WebSocket.
WebSocket manager rewritten based on roslibPY library using standard methods, for example:
```python
topic = roslibpy.Topic( self.ws, topic, topic_data_type )
```
Instead of regular network interaction in the original through JSON:
```python
# Ensure message is JSON serializable
json_msg = json.dumps(message)
self.ws.send(json_msg) 
```
### Added Voice Agent for Seamless Control
Voice agent extracted into a separate Python file – voice_agent.py for running both on the robot itself and on a separate station.

Voice command activation training completed for "Brewie" using Porcupine Wake Word Python API. Models prepared for running on Windows PC and Raspberry PI5 robot:
* Brewie_en_raspberry-pi_v3_0_0.ppn
* Brewie_en_windows_v3_0_0.ppn

When building, specify the appropriate model for your chosen platform.

Wake Word provides quick response to robot interaction with minimal resources.

After activation, recording and recognition of robot interaction is performed through the SpeechRecognition package.

Next, the text interpretation of the user's request is passed to the LLM. A system prompt is pre-formed and chat history is optionally saved for context (history_active flag). Voice recognition can be disabled and text chat mode selected through the text_input flag (true to disable voice input).

LLM work is performed through the Together API (https://together.ai/), any model available for your API key can be selected.

Response voicing is implemented through gTTS.

To reduce delay time, caching of previously voiced responses within the session has been added.
LLM response hash checking is performed and in case of such in cache, local recording is played.

### MCP passes Brewie native application Action group files to LLM context.
Now LLM can access previously created files with robot actions (ActionGroups) in the editor and call them according to context. For this, a tool is implemented in the MCP server get_available_actions()
Detailed description of added and modified functions is in MCPFUNCTIONS.md

It's important to give prepared actions clear names for adequate LLM context perception. If done correctly, AI will be able to call the right action by description or situation, without requiring the user to know the exact name.

## You'll Need API Keys!

For https://together.ai/ and https://console.picovoice.ai/ (quick voice activation). Fortunately, they can be obtained for free by registering on the sites.

Keys are passed through environment variables during startup.

## Quick Start

Run the ROS/action\_groups.py file on the robot to publish current actions, first on the robot then in docker

```bash
docker cp action_groups.py brewie:/home/ubuntu/ros_ws/src
```

Now deploy the MCP server on the robot or PC (PC must be on the same network as the robot or you'll need to connect a microphone to the robot. If necessary, adjust the ROS IP for network operation.

MCP communicates with the agent through STDIO, so it's enough to call the voice agent, it will start the server itself.

UV is used for convenient package installation

To run everything, use the template bat file adding your API keys to it

```bash
set TOGETHER_API_KEY=Your key
set WAKEUP_API_KEY=Your key
uv run voice_agent.py
```

On first run, necessary packages will be installed

Now you're ready to experience your robot in a new way with LLM!
