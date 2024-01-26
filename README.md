# 대양고등학교 급식 조회 API
```python
import requests
from bs4 import BeautifulSoup
from flask import Flask, Response

schoolURL = "https://school.busanedu.net/daeyang-h/main.do"

def getMeal():
    res = requests.get(schoolURL)
    soup = BeautifulSoup(res.content, 'html.parser')
    mealList = soup.select_one('.meal_list').text
    return mealList

app = Flask(__name__)

@app.route("/", methods=["GET"])
def main():
    try:
        meal = getMeal()
        return "\n" + meal + "\n" + "\n"
    except Exception as e:
        print(e)
        return "<h1>오류가 발생하였습니다.</h1><h2>API 콘솔을 확인하여 주시기 바랍니다.</h2>", 500

if __name__ == '__main__':
    app.run(host="0.0.0.0", port=80)
```

# How to Run?

https://github.com/jeonilshin/daeyang-lunch-api/assets/86287920/f65c58cb-7f43-42ef-9ad5-d5bb14279acd

