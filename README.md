# hello-world
only a start
import requests
import re
import pandas as pd
import matplotlib.pyplot as plt

def retrieve_dji_list():
    r = requests.get('http://money.cnn.com/data/dow30/')
    search_pattern = re.compile('class="wsod_symbol">(.*?)<\/a>.*?<span.*?">(.*?)<\/span>.*?\n.*class="wsod_stream">(.*?)<\/span>')
    dji_list_in_text = re.findall(search_pattern, r.text)
    return dji_list_in_text

dji_list = retrieve_dji_list()
dji_table = pd.DataFrame(dji_list)
cols = ['code','name','lasttrade']
dji_table.columns = cols
dji_table.index = range(1,len(dji_list)+1)
print(dji_table)
