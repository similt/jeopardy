import pandas as pd
jeopardy = pd.read_csv("jeopardy.csv")
jeopardy.columns=jeopardy.columns.str.replace(" ","")
import re

def normalize_text(text):
    text = text.lower()
    text = re.sub("[^A-Za-z0-9\s]", "", text)
    text = re.sub("\s+", " ", text)
    return text
jeopardy["clean_question"] = jeopardy["Question"].apply(normalize_text)
jeopardy["clean_answer"] = jeopardy["Answer"].apply(normalize_text)
jeopardy.info()
import re
def strnorm(text):
    text=re.sub('\W',"",text)
    try:
        text=int(text)
    except: 
        text=0 
    return text 
#strnorm("$90500")
jeopardy["AirDate"]=pd.to_datetime(jeopardy["AirDate"])
def sfunc(row):
    split_answer=row["clean_answer"].split()
    split_question=row["clean_question"].split()
    match_count=0
    if 'the' in split_answer: 
        split_answer.remove('the')
    if len(split_answer)==0:
        return 0
    for ans in split_answer: 
        if ans in split_question: 
            match_count+=1
    return match_count/len(split_answer)
aa=jeopardy.apply(sfunc,axis=1)
answer_in_question =aa.mean()

jeopardy.sort_values("AirDate",inplace=True)
question_overlap=[]
terms_used=set()
for index,row in jeopardy.iterrows():
    #print(index,data)
    split_question=row['clean_question'].split()
    split_question=[x for x in split_question if len(x)>5 ]
    match_count =0 
    for word in split_question:
        if word in terms_used: 
            match_count+=1
        #else: 
        terms_used.add(word)
    if len(split_question)>0: 
        match_count=match_count/len(split_question)
    question_overlap.append(match_count)
jeopardy["question_overlap"] = question_overlap
jeopardy["question_overlap"].mean()

def valuea(row):
    if row["clean_value"]>800: 
        value=1
    else: 
        value=0 
    return value
jeopardy["high_value"]=jeopardy.apply(valuea,axis=1)


def valuecnt(word):
    low_count=0
    high_count=0
    for index,row in jeopardy.iterrows():
        split_question=row['clean_question'].split()
        if word in split_question:
            if row['high_value']==1: 
                high_count+=1
            else:
                low_count+=1 
    return high_count,low_count
    
  import random 
terms_used=list(terms_used)
comparison_terms= [random.choice(terms_used) for x in range(10)]
comparison_terms
observed_expected=[]
for item in comparison_terms: 
    observed_expected.append(valuecnt(item))
observed_expected
