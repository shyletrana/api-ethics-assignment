full_name-(direct PII and drop) directly identifies an individual
email-(direct PII and drop) Unique identifier
date_of_birth-(indirect PII and mask) year is enough for analysis
zip_code -( Indirect PII and Mask)  partial keeps regional insights
job_title-(Indirect PII and Pseudonymize) low risk if generalized 
diagnosis_notes-(direct PII and  Pseudonymize) high risk only for personal details we can keep report as it is.


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
