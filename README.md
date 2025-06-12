import streamlit as st
import pandas as pd
import datetime

st.title('📅 나만의 시간표 & D-day 관리')

days = ['월', '화', '수', '목', '금']
periods = [f"{i+1}교시" for i in range(7)]
timetable = {}

for day in days:
    st.header(f'{day}요일')
    timetable[day] = []
    for period in periods:
        subject = st.text_input(f'{day} {period}', key=f'{day}{period}')
        timetable[day].append(subject)

st.header('⏰ D-day 관리')
dday_name = st.text_input('D-day 이름')
dday_date = st.date_input('D-day 날짜')
if st.button('D-day 추가'):
    d = (dday_date - datetime.date.today()).days
    st.success(f'D-{d}: {dday_name}')

st.header('📋 현재 시간표')
df = pd.DataFrame(timetable, index=periods).T
st.dataframe(df)
# -
