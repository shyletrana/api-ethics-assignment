import time
import requests
import os
API_URL="https://healthstats-api.example.com/records"
API_KEY=os.getenv("API_KEY")
records=[]
MAX_PAGES=10
for page in range(1,MAX_PAGES+1):
  response=requests.get(API_URL,params={"page":page,"key":API_KEY})
  if response.status_code != 200:
   break
  data=response.json()
  records.extend(data.get("res",[]))
  time.sleep(1)
save_to_database(records)
