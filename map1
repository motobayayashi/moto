# モジュールのインポート
import pandas as pd
import urllib
import urllib.error
import urllib.request
from pygeocoder import Geocoder
import googlemaps
from linebot import LineBotApi
from linebot.models import TextSendMessage, ImageSendMessage

# パラメータの設定
googleapikey = '取得したGoogleのAPIキー'
line_channel_access_token = '取得したLINEのチャネルアクセストークン'
output_path = '出力先のフォルダのパス'
pixel = '640x480'
scale = '18'

# LINE APIの初期化
line_bot_api = LineBotApi(line_channel_access_token)

# GPS端末からリアルタイムに取得する緯度、経度のデータ
# ここでは仮のデータを使用します
lat = 35.6895
lng = 139.6917

# Google Maps APIを使用して位置情報と航空写真を取得する関数
def get_location_image(lat, lng):
    html1 = '5'
    html2 = '&maptype=hybrid'
    html3 = '&size='
    html4 = '&sensor=false'
    html5 = '&zoom='
    html6 = '&markers='
    html7 = '&key='
    axis = str(lat) + "," + str(lng)
    url = html1 + axis + html2 + html3 + pixel + html4 + html5 + scale + html6 + axis + html7 + googleapikey
    dst_path = output_path + '\\' + "location.png"
    try:
        data = urllib.request.urlopen(url).read()
        with open(dst_path, mode="wb") as f:
            f.write(data)
    except urllib.error.URLError as e:
        print(e)
    return dst_path

# LINEのトーク画面に位置情報を送信する関数
def send_location_to_line(user_id, image_path):
    image_message = ImageSendMessage(
        original_content_url=image_path,
        preview_image_url=image_path
    )
    line_bot_api.push_message(user_id, image_message)

# メインの処理
image_path = get_location_image(lat, lng)
send_location_to_line('ユーザーID', image_path)
