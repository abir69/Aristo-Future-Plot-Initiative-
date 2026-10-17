import os
import streamlit as st
import google.generativeai as genai

st.set_page_config(page_title="My AI App", page_icon="🤖")
st.title("My Live AI App")

# API Setup
api_key = os.environ.get("GEMINI_API_KEY")
if not api_key:
    st.error("API Key সেট করা হয়নি!")
    st.stop()

genai.configure(api_key=api_key)
model = genai.GenerativeModel("gemini-1.5-flash")

# Chat Interface
if "messages" not in st.session_state:
    st.session_state.messages = []

for message in st.session_state.messages:
    with st.chat_message(message["role"]):
        st.markdown(message["content"])

if user_input := st.chat_input("কিছু লিখুন..."):
    st.session_state.messages.append({"role": "user", "content": user_input})
    with st.chat_message("user"):
        st.markdown(user_input)

    response = model.generate_content(user_input)
    st.session_state.messages.append({"role": "assistant", "content": response.text})
    with st.chat_message("assistant"):
        st.markdown(response.text)
