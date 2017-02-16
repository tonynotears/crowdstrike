import requests
import datetime
import json
import csv
import sys

today = datetime.date.today()
oneweek = (today - datetime.timedelta(days=7)).strftime("%Y-%m-%d")

username = "<username>"
password = "<password>"
url = "https://falconapi.crowdstrike.com/devices/queries/devices/v1?filter=last_seen:<" + "\'" + oneweek + "\'"
r = requests.get(url,auth=(username,password))
stream = r.text
text = json.loads(stream)
reporter = csv.writer(sys.stdout)
reporter.writerow(("HostName","Last_Seen","OS_Version"))

for aid in text['resources']:
    url1 = "https://falconapi.crowdstrike.com/devices/entities/devices/v1?ids=" + aid
    r1 = requests.get(url1, auth=(username, password))
    report = r1.text
    result = json.loads(report)
    for host in result['resources']:
        reporter.writerow ([
            host['hostname'],
            host['last_seen'],
            host['os_version'],
        ])
