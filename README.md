English| [简体中文](./README_cn.md)

# GPTNode

**gpt_node** provides interaction with ChatGPT, subscribes to text messages, calls the ChatGPT API to get results, and then sends out the results. Currently supports two interaction modes. One is chat mode, where historical conversations are added to ChatGPT for multi-turn dialogue. This mode consumes more tokens. The other mode is question-answering mode, supporting only single-turn dialogue where the user asks ChatGPT a question and receives an answer, starting a new dialogue each time. Interaction mode can be configured through the `chat_mode_enable` field in the *gpt_config.json* configuration file, with the default mode being question-answering mode.

## Running Instructions
1. Copy the configuration file to the current directory

   tros foxy:
   ```bash
   cp -rf /opt/tros/lib/gpt_node/config ./
   ```

   tros humble:
   ```bash
   cp -rf /opt/tros/${TROS_DISTRO}/lib/gpt_node/config ./
   ```

2. Modify *config/gpt_config.json* to set the **api_key** field to your own ChatGPT API Key

3. Ensure network connectivity to ChatGPT is available

4. Run the Node

   tros foxy:
   ```bash
   # Configure the tros.b environment:
   source /opt/tros/setup.bash
   # run to start
   ros2 run gpt_node gpt_node
   ```

   tros humble:
   ```bash
   # Configure the tros.b humble environment:
   source /opt/tros/humble/setup.bash
   # run to start
   ros2 run gpt_node gpt_node
   ```

   After the program runs successfully, it subscribes to the topic "/request_text" (std_msgs/msg/String type) by default and publishes the results to the topic "/response_text" (std_msgs/msg/String type).

   You can use the following command to send a message to verify if the program is running successfully:

   tros foxy:
   ```bash
   # Configure the tros.b humble environment:
   source /opt/tros/setup.bash
   ros2 topic pub --once /request_text std_msgs/msg/String "{data: "你是谁"}"
   ```
   tros humble:
   ```bash
   # Configure the tros.b humble environment:
   source /opt/tros/humble/setup.bash
   ros2 topic pub --once /request_text std_msgs/msg/String "{data: "你是谁"}"
   ```

   Note: Regular user ChatGPT API Keys have frequency limits, generally restricted to three times per minute.

## Parameter List
| Parameter Name  | Description     | Type        | Required  | Default Value |
| --------------- | --------------  | ----------- | --------  | -----------   |
| gpt_topic_sub   | Subscribed text topic | std::string | No     | "/request_text" |
| gpt_topic_pub   | Published text topic  | std::string | No     | "/response_text" |