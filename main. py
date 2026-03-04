import streamlit as st
from google import genai

st.set_page_config(page_title="AI Resume Analyzer", page_icon="📄")

st.title("📄 AI Resume Analyzer")
st.write("Paste your resume and job description to get instant AI feedback!")

api_key = st.text_input("Enter your Gemini API Key", type="password")
resume_text = st.text_area("Paste Your Resume Here", height=200)
job_description = st.text_area("Paste Job Description Here", height=200)

def analyze_resume(resume, job_desc, api_key):
    client = genai.Client(api_key=api_key)
    prompt = f"""
    You are an expert ATS Resume Analyzer and Career Coach.
    Analyze the resume against the job description below.

    ## 🎯 ATS Match Score
    Give a score out of 100 based on how well the resume matches the job description.

    ## ❌ Missing Keywords
    List the important keywords from the job description that are missing in the resume.

    ## ✏️ Rewrite Suggestions
    Give exactly 3 specific rewrite suggestions with:
    - BEFORE: (original text)
    - AFTER: (improved text)
    - WHY: (reason for change)

    ## 📊 Overall Grade
    Give a grade: A, B, C, or D with a short reason.

    ## 💡 Final Advice
    2-3 sentences of actionable advice to improve this resume.

    RESUME:
    {resume}

    JOB DESCRIPTION:
    {job_desc}
    """
    response = client.models.generate_content(
        model="gemini-2.0-flash",
        contents=prompt
    )
    return response.text

if st.button("Analyze Resume 🚀"):
    if not api_key or not resume_text or not job_description:
        st.warning("Please fill in all three fields!")
    else:
        with st.spinner("AI is analyzing your resume..."):
            try:
                result = analyze_resume(resume_text, job_description, api_key)
                st.success("Analysis Complete! ✅")
                st.markdown(result)
            except Exception as e:
                st.error(f"Error: {str(e)}")

st.markdown("---")
st.markdown("Built with ❤️ by Pitchaiah | Powered by Google Gemini AI")
