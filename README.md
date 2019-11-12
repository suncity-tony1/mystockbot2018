# mystockbot2018
from flask import Flask, request, abort

from linebot import (
    LineBotApi, WebhookHandler
)
from linebot.exceptions import (
    InvalidSignatureError
)
from linebot.models import *

app = Flask(__name__)

# 必須放上自己的Channel Access Token
line_bot_api = LineBotApi('lHblUneNdycfWUAc4imGaRHmef3bW84GWZv8bHs7u+kdCZhipvDCj/aB+IlOnaYtuFaw/nVs+j0htocSNCw4KnT5hI5hJ44b3i1zMysbwxU8vKZ7Oo29ubctx7++IyGGRLdw3HfyYAm7XfkEeKQwsQdB04t89/1O/w1cDnyilFU=')

# 必須放上自己的Channel Secret
handler = WebhookHandler('c0560ec2216b5a6f89a5901e8690a4f0')

line_bot_api.push_message('Ub67359922c67178045b3a8e29c960401', TextSendMessage(text='你可以開始了'))

# 監聽所有來自 /callback 的 Post Request
@app.route("/callback", methods=['POST'])
def callback():
    # get X-Line-Signature header value
    signature = request.headers['X-Line-Signature']

    # get request body as text
    body = request.get_data(as_text=True)
    app.logger.info("Request body: " + body)
