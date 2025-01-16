# Dify Node.js SDK Plus
This is the Node.js SDK for the Dify APIS, which allows you to easily integrate Dify into your Node.js applications.

## Install
```bash
npm install dify-client-plus
```

## Usage
After installing the SDK, you can use it in your project like this:

```js
import { DifyClient, ChatClient, CompletionClient } from 'dify-client-plus'

const API_KEY = 'your-api-key-here'
const user = `random-user-id`
const query = 'Please tell me a short story in 10 words or less.'
const remote_url_files = [{
    type: 'image',
    transfer_method: 'remote_url',
    url: 'your_url_addresss'
}]

// Create a completion client
const completionClient = new CompletionClient(API_KEY)
// Create a completion message
completionClient.createCompletionMessage({'query': query}, user)
// Create a completion message with vision model
completionClient.createCompletionMessage({'query': 'Describe the picture.'}, user, false, remote_url_files)

// Create a chat client
const chatClient = new ChatClient(API_KEY)
// Create a chat message in stream mode
const response = await chatClient.createChatMessage({}, query, user, true, null)
const stream = response.data;
stream.on('data', data => {
    console.log(data);
});
stream.on('end', () => {
    console.log('stream done');
});
// Create a chat message with vision model
chatClient.createChatMessage({}, 'Describe the picture.', user, false, null, remote_url_files)
// Fetch conversations
chatClient.getConversations(user)
// Fetch conversation messages
chatClient.getConversationMessages(conversationId, user)
// Rename conversation
chatClient.renameConversation(conversationId, name, user)


const client = new DifyClient(API_KEY)
// Fetch application parameters
client.getApplicationParameters(user)
// Provide feedback for a message
client.messageFeedback(messageId, rating, user)

```

Replace 'your-api-key-here' with your actual Dify API key.Replace 'your-app-id-here' with your actual Dify APP ID.

## APIS 

### ChatFlow
- [x] 发送对话消息 createChatMessage
- [x] 停止响应 stopChat
- [x] 消息反馈（点赞） feedback
- [x] 获取下一轮建议问题列表 getSuggested
- [x] 获取会话历史消息 getConversationMessages
- [x] 获取会话列表 getConversations
- [x] 删除会话 deleteConversation
- [x] 会话重命名 renameConversation
- [x] 语音转文字 aduioToText
- [x] 文字转语音 textToAudio
- [x] 获取应用Meta信息 getMeta
- [] ~~completion-messages~~

### ChatFlow
- [x] 执行 workflow runWorkflow
- [x] 获取workflow执行情况 checkWorkflow
- [x] 停止响应 stopWorkflow
- [x] 获取 workflow 日志 getWorkflowLogs

### Commons
- [x] 上传文件 fileUpload
- [x] 获取应用基本信息 getInfo
- [x] 获取应用参数 application

## License
This SDK is released under the MIT License.
