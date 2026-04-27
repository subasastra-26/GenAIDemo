import streamlit as st
from llm_chain import translate_text

# ---------- PAGE CONFIG ----------
st.set_page_config(
    page_title="AI Smart Translator",
    layout="wide"
)

# ---------- CSS (SAAS STYLE UI) ----------
st.markdown("""
<style>
body {
    background-color: #0e1117;
}

.main-title {
    text-align: center;
    font-size: 40px;
    font-weight: 800;
    background: linear-gradient(to right, #00c6ff, #0072ff);
    -webkit-background-clip: text;
    color: transparent;
    margin-bottom: 10px;
}

.subtitle {
    text-align: center;
    color: #aaa;
    margin-bottom: 20px;
}

.card {
    background-color: #1c1f26;
    padding: 18px;
    border-radius: 12px;
    margin-top: 15px;
    color: white;
    box-shadow: 0px 4px 15px rgba(0,0,0,0.3);
}

textarea {
    background-color: #1c1f26 !important;
    color: white !important;
    border-radius: 10px;
}

div.stButton > button {
    background-color: #0072ff;
    color: white;
    border-radius: 10px;
    height: 3em;
    font-size: 16px;
}
</style>
""", unsafe_allow_html=True)

# ---------- HEADER ----------
st.markdown("<div class='main-title'>🌍 AI Smart Translator</div>", unsafe_allow_html=True)
st.markdown("<div class='subtitle'>AI Powered</div>", unsafe_allow_html=True)

# ---------- SIDEBAR ----------
st.sidebar.title("⚙️ Translation Mode")

mode = st.sidebar.radio(
    "Choose Mode",
    [
        "Tamil → English",
        "English → Tamil",
        "Tanglish → English",
        "Hindi → English",
        "English → Hindi",
        "Telugu → English",
        "English → Telugu"
    ]
)

st.sidebar.markdown("---")
#st.sidebar.info("💡 Tip: Paste WhatsApp chats or normal text for best results")

# ---------- INPUT ----------
st.markdown("### ✍️ Enter Text")



if "text_input" not in st.session_state:
    st.session_state.text_input = ""


text_input = st.text_area(
    "",
    height=200,
    placeholder="Type Tamil / English / Hindi / Telugu / Tanglish..."
)

# ---------- BUTTON ----------
translate_btn = st.button("🚀 Translate Now")

# ---------- OUTPUT ----------
if translate_btn:
    if text_input.strip():

        with st.spinner("🧠 AI is translating..."):
            result = translate_text(text_input, mode)

        st.markdown("### 🌐 Result")

        st.markdown(f"""
        <div class="card">
        {result}
        </div>
        """, unsafe_allow_html=True)

    else:
        st.warning("⚠️ Please enter some text to translate")
