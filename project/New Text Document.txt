import streamlit as st
from groq import Groq

# ---------------------------
# GROQ API SETUP
# ---------------------------
client = Groq(
    api_key="YOUR_GROQ_API_KEY"
)

# ---------------------------
# PAGE CONFIG
# ---------------------------
st.set_page_config(
    page_title="BrandCraft",
    page_icon="🎨",
    layout="wide"
)

# ---------------------------
# SIDEBAR
# ---------------------------
st.sidebar.title("🎨 BrandCraft")

menu = st.sidebar.radio(
    "Navigation",
    ["Home", "Brand Name Generator", "Slogan Generator", "Brand Guidelines"]
)

# ---------------------------
# HOME PAGE
# ---------------------------
if menu == "Home":

    st.title("BrandCraft : Generative AI–Powered Branding Automation System")

    st.write(
        """
        Welcome to **BrandCraft** 🚀  
        Create powerful brand identities using **AI powered by Groq**.
        """
    )

    col1, col2, col3 = st.columns(3)

    with col1:
        st.subheader("Brand Name Generator")
        st.write("Generate unique brand names instantly")

    with col2:
        st.subheader("Slogan Creator")
        st.write("Create catchy brand slogans")

    with col3:
        st.subheader("Brand Guidelines")
        st.write("Generate brand strategy and identity")

# ---------------------------
# BRAND NAME GENERATOR
# ---------------------------
elif menu == "Brand Name Generator":

    st.header("AI Brand Name Generator")

    business_type = st.text_input("Enter your business type")

    if st.button("Generate Brand Names"):

        prompt = f"""
        Generate 10 creative brand names for a {business_type} business.
        """

        chat_completion = client.chat.completions.create(
            messages=[
                {"role": "user", "content": prompt}
            ],
            model="llama3-8b-8192",
        )

        result = chat_completion.choices[0].message.content
        st.success(result)

# ---------------------------
# SLOGAN GENERATOR
# ---------------------------
elif menu == "Slogan Generator":

    st.header("AI Slogan Generator")

    brand_name = st.text_input("Enter Brand Name")
    brand_description = st.text_area("Describe your brand")

    if st.button("Generate Slogans"):

        prompt = f"""
        Create 10 catchy slogans for a brand called {brand_name}.
        Brand description: {brand_description}
        """

        chat_completion = client.chat.completions.create(
            messages=[
                {"role": "user", "content": prompt}
            ],
            model="llama3-8b-8192",
        )

        result = chat_completion.choices[0].message.content
        st.success(result)

# ---------------------------
# BRAND GUIDELINES
# ---------------------------
elif menu == "Brand Guidelines":

    st.header("AI Brand Kit Generator")

    brand = st.text_input("Brand Name")
    industry = st.text_input("Industry")
    target = st.text_input("Target Audience")

    if st.button("Generate Brand Kit"):

        prompt = f"""
        Create a brand guideline for the brand {brand} in the {industry} industry.
        Target audience: {target}

        Include:
        - Brand mission
        - Brand vision
        - Color palette
        - Typography
        - Brand tone
        - Logo ideas
        """

        chat_completion = client.chat.completions.create(
            messages=[
                {"role": "user", "content": prompt}
            ],
            model="llama3-8b-8192",
        )

        result = chat_completion.choices[0].message.content
        st.success(result)