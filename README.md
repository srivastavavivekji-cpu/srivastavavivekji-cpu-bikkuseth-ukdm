import streamlit as st
import google.generativeai as genai

st.set_page_config(page_title="Bikkuseth's (UKDM Engine)", page_icon="🧠")
st.title("🧠 Bikkuseth's (UKDM Engine)")
st.caption("Universal Knowledge & Discovery Model v3.0 Powered Solver")

# API Key Config
try:
    genai.configure(api_key=st.secrets["GEMINI_API_KEY"])
    model = genai.GenerativeModel('gemini-1.5-flash')
except Exception as e:
    st.error("कृपया Streamlit Secrets में GEMINI_API_KEY सेट करें।")

user_problem = st.text_area("अपनी समस्या या प्रोजेक्ट दर्ज करें:", placeholder="उदाहरण: मेरी दुकान की बिक्री नहीं बढ़ रही है...")

if st.button("🚀 Bikkuseth से समाधान पूछें"):
    if user_problem:
        with st.spinner("भिक्कू सेठ हिसाब लगा रहे हैं..."):
            prompt = f"""
            You are Bikkuseth's (UKDM Engine), an expert system solver using UKDM v3.0 framework.
            Analyze the following problem and provide a structured answer in Hindi:
            Problem: {user_problem}
            
            Structure:
            1. Core Analysis (Constraints & Primary Unit)
            2. System Flow / Visual Mapping
            3. Actionable 3-Step Plan
            """
            response = model.generate_content(prompt)
            st.success("✅ विश्लेषण पूर्ण हुआ!")
            st.markdown(response.text)
    else:
        st.warning("कृपया पहले अपनी समस्या लिखें!")
