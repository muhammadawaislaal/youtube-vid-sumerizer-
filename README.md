
</div>

## 📋 Table of Contents
- [✨ Features](#features)
- [🚀 Quick Start](#quick-start)
- [📁 Project Structure](#project-structure)
- [🛠️ Installation](#installation)
- [⚙️ Configuration](#configuration)
- [📺 Usage Guide](#usage-guide)
- [🤖 AI Models](#ai-models)
- [📝 Transcript Extraction](#transcript-extraction)
- [🔧 Fallback Systems](#fallback-systems)
- [🎨 UI/UX Features](#uiux-features)
- [🔒 Security](#security)
- [🚀 Deployment](#deployment)
- [🤝 Contributing](#contributing)
- [📄 License](#license)
- [⚠️ Disclaimer](#disclaimer)
- [👨‍💻 Developer](#developer)

## ✨ Features

### 🎯 Core Features
- **📺 YouTube Integration** - Extract transcripts from any public YouTube video
- **🤖 Multi-AI Support** - OpenAI GPT-3.5 & Groq LLaMA 3.1 integration
- **⚡ Intelligent Summarization** - Context-aware, coherent video summaries
- **🔄 Multi-Method Transcript Extraction** - Multiple approaches for reliability
- **📊 Word Count Analysis** - Track transcript and summary lengths

### 🛡️ Professional Features
- **🔑 Flexible API Configuration** - Multiple API key management methods
- **🎯 Provider Selection** - Choose between OpenAI and Groq APIs
- **📝 Raw Transcript Viewing** - Access full extracted transcripts
- **💾 Summary Export** - Copy summaries directly from interface
- **🔍 Video Preview** - Embedded YouTube player integration

### 🚀 Technical Highlights
- Multi-layer transcript extraction with fallbacks
- Intelligent text truncation for API limits
- Comprehensive error handling with user-friendly messages
- Session state management for user persistence
- Automatic dependency installation

## 📁 Project Structure

```
youtube-summarizer/
├── app.py                              # Main Streamlit application
├── requirements.txt                    # Python dependencies
├── README.md                           # Project documentation
├── .streamlit/                         # Streamlit configuration
│   ├── config.toml                    # App configuration
│   └── secrets.toml                   # API keys (gitignored)
│
├── utils/                              # Utility functions
│   ├── transcript_extractor.py        # YouTube transcript extraction
│   ├── ai_summarizer.py              # AI summarization logic
│   ├── video_processor.py            # Video ID extraction and metadata
│   ├── fallback_system.py            # Fallback summarization methods
│   └── api_manager.py                # API client management
│
├── tests/                              # Test files
│   ├── test_transcript_extraction.py  # Transcript extraction tests
│   ├── test_summarization.py         # Summarization algorithm tests
│   ├── test_api_integration.py       # API connection tests
│   └── test_video_parsing.py         # YouTube URL parsing tests
│
├── docs/                               # Documentation
│   ├── api_reference.md              # API documentation
│   ├── transcript_methods.md         # Transcript extraction methods
│   └── deployment_guide.md           # Deployment instructions
│
└── examples/                           # Example usage
    ├── example_transcripts.txt       # Sample transcripts
    └── example_summaries.txt         # Sample AI summaries
```

## 🚀 Quick Start

### Prerequisites
- Python 3.9+
- YouTube video URL (public)
- API key from OpenAI or Groq (optional, for enhanced features)

### One-Line Installation
```bash
git clone https://github.com/muhammadawaislaal/youtube-summarizer.git && cd youtube-summarizer && pip install -r requirements.txt && streamlit run app.py
```

## 🛠️ Installation

### Method 1: Standard Installation
```bash
# Clone the repository
git clone https://github.com/muhammadawaislaal/youtube-summarizer.git
cd youtube-summarizer

# Create virtual environment
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# Mac/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Run the application
streamlit run app.py
```

### Method 2: Docker Installation
```dockerfile
# Dockerfile
FROM python:3.9-slim
WORKDIR /app

# Install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application
COPY . .

# Expose port
EXPOSE 8501

# Run application
CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]
```

```bash
# Build and run
docker build -t youtube-summarizer .
docker run -p 8501:8501 youtube-summarizer
```

## ⚙️ Configuration

### API Key Setup
Create `.streamlit/secrets.toml` for API keys:
```toml
# .streamlit/secrets.toml
OPENAI_API_KEY = "your_openai_api_key_here"
GROQ_API_KEY = "your_groq_api_key_here"

# Alternative format
[openai]
api_key = "your_openai_api_key_here"

[groq]
api_key = "your_groq_api_key_here"
```

### Application Configuration
```python
# API Provider Configuration
API_CONFIGS = {
    "openai": {
        "model": "gpt-3.5-turbo",
        "max_tokens": 500,
        "temperature": 0.3
    },
    "groq": {
        "model": "llama-3.1-8b-instant",
        "max_tokens": 500,
        "temperature": 0.3
    }
}

# Transcript Extraction Settings
TRANSCRIPT_CONFIG = {
    "max_length": 12000,  # Characters for API truncation
    "timeout": 15,        # Request timeout in seconds
    "retry_attempts": 3   # Number of retry attempts
}
```

### Environment Variables
```bash
# Set environment variables (alternative to secrets.toml)
export OPENAI_API_KEY="your_openai_api_key_here"
export GROQ_API_KEY="your_groq_api_key_here"
```

## 📺 Usage Guide

### 1. Getting Started
1. **Launch Application**: Run `streamlit run app.py`
2. **Access Interface**: Open browser to `http://localhost:8501`
3. **Configure API Keys**: Set up OpenAI or Groq API keys (optional)

### 2. API Key Configuration
#### Option A: Streamlit Secrets
1. Create `.streamlit/secrets.toml` file
2. Add API keys in correct format
3. Restart application

#### Option B: Manual Input
1. Click "API Key Configuration" expander
2. Select API provider (OpenAI or Groq)
3. Enter API key in password field
4. Click to verify connection

#### Option C: Environment Variables
1. Set environment variables in terminal
2. Restart application
3. Keys will be auto-detected

### 3. Generating Summaries
#### Step 1: Enter YouTube URL
```
Supported URL formats:
- https://www.youtube.com/watch?v=VIDEO_ID
- https://youtu.be/VIDEO_ID
- https://youtube.com/watch?v=VIDEO_ID
```

#### Step 2: Generate Summary
1. Click "Generate Summary" button
2. View progress indicators:
   - Video ID extraction
   - Transcript fetching
   - AI summarization

#### Step 3: Review Results
1. **Video Preview**: Embedded YouTube player
2. **Transcript Status**: Extraction method and word count
3. **AI Summary**: Intelligent video summary
4. **Raw Transcript**: Full transcript in expandable section

### 4. Working Without API Keys
- **Fallback Mode**: Uses local summarization algorithm
- **Basic Functionality**: Extract transcripts without AI enhancement
- **Manual Summarization**: Copy transcript for manual processing

## 🤖 AI Models

### Supported AI Providers
```python
# OpenAI Configuration
OPENAI_CONFIG = {
    "model": "gpt-3.5-turbo",
    "max_tokens": 500,
    "temperature": 0.3,
    "system_prompt": "You are a helpful assistant that creates accurate and concise summaries of video content."
}

# Groq Configuration
GROQ_CONFIG = {
    "model": "llama-3.1-8b-instant",
    "max_tokens": 500,
    "temperature": 0.3,
    "system_prompt": "You are a helpful assistant that creates accurate and concise summaries of video content."
}
```

### Summarization Prompt Engineering
```python
SUMMARIZATION_PROMPT = """
Please provide a comprehensive and accurate summary of the following video transcript from a video titled "{video_title}". 
Focus on the main points, key insights, and important information. 
Make the summary concise but informative, capturing the essence of the content.

Transcript:
{transcript}

Summary:
"""
```

### Model Comparison
| Feature | OpenAI GPT-3.5 | Groq LLaMA 3.1 |
|---------|----------------|----------------|
| **Speed** | Moderate | Very Fast |
| **Cost** | Per token usage | Free tier available |
| **Context** | 4K tokens | 8K tokens |
| **Quality** | Excellent | Very Good |
| **Availability** | Requires paid API | Free tier with limits |

## 📝 Transcript Extraction

### Multi-Method Extraction System
```python
def extract_transcript(video_id):
    """Multi-layer transcript extraction strategy"""
    
    # Method 1: Official YouTube caption tracks
    transcript = try_official_captions(video_id)
    if transcript: return transcript, "Official Captions"
    
    # Method 2: Alternative transcript services
    transcript = try_alternative_services(video_id)
    if transcript: return transcript, "Alternative Service"
    
    # Method 3: Web scraping and parsing
    transcript = try_web_scraping(video_id)
    if transcript: return transcript, "Web Scraping"
    
    # Method 4: Simulated transcript based on metadata
    transcript = generate_simulated_transcript(video_id)
    return transcript, "Simulated Transcript"
```

### Extraction Methods
1. **Official YouTube Captions**:
   - Direct access to YouTube's caption tracks
   - Supports multiple languages
   - Highest quality when available

2. **Alternative Services**:
   - Third-party transcript services
   - Multiple endpoint fallbacks
   - Community-maintained sources

3. **Web Scraping**:
   - HTML parsing of YouTube pages
   - JavaScript rendering detection
   - Multiple user-agent rotation

4. **Simulated Transcript**:
   - Fallback when other methods fail
   - Based on video metadata
   - Educational placeholder content

### Error Handling
- **Timeout Management**: Configurable request timeouts
- **Retry Logic**: Multiple attempts with exponential backoff
- **Graceful Degradation**: Fallback to simpler methods
- **User Feedback**: Clear status messages and error explanations

## 🔧 Fallback Systems

### Multi-Layer Architecture
```python
def summarize_with_fallback(transcript, video_title):
    """Intelligent fallback summarization system"""
    
    # Layer 1: Primary API (OpenAI or Groq based on configuration)
    if api_available():
        summary = summarize_with_api(transcript, video_title)
        if summary: return summary, "AI Generated"
    
    # Layer 2: Alternative API (switch provider)
    if alternative_api_available():
        summary = summarize_with_alternative_api(transcript, video_title)
        if summary: return summary, "Alternative AI"
    
    # Layer 3: Local Summarization Algorithm
    summary = local_summarization_algorithm(transcript)
    return summary, "Local Algorithm"
```

### Local Summarization Algorithm
```python
def local_summarization_algorithm(text):
    """Rule-based summarization for API fallback"""
    
    # Step 1: Sentence segmentation
    sentences = split_into_sentences(text)
    
    # Step 2: Sentence scoring
    scored_sentences = score_sentences(sentences, factors=[
        "position", "length", "keywords", "uniqueness"
    ])
    
    # Step 3: Sentence selection
    selected_sentences = select_top_sentences(scored_sentences)
    
    # Step 4: Summary construction
    summary = reconstruct_summary(selected_sentences)
    
    return summary
```

### Error Recovery Strategies
1. **API Rate Limit Handling**: Automatic retry with delay
2. **Token Limit Management**: Intelligent text truncation
3. **Network Failure Recovery**: Multiple endpoint fallbacks
4. **Authentication Error Handling**: Clear user guidance for key issues

## 🎨 UI/UX Features

### Sidebar Information Panel
- **Project Overview**: Application description and features
- **Setup Instructions**: Step-by-step installation guide
- **Usage Guide**: How to use the application effectively
- **Developer Information**: Contact and attribution details

### Main Interface Components
1. **Header Section**:
   - Application title and description
   - Clear navigation and branding

2. **Input Section**:
   - YouTube URL input field
   - Example URLs for testing
   - Generate button with primary styling

3. **Progress Indicators**:
   - Spinner animations during processing
   - Success/error status messages
   - Step-by-step progress visualization

4. **Results Display**:
   - Video preview with embedded player
   - Transcript status and word count
   - AI-generated summary
   - Copy-to-clipboard functionality

### Visual Feedback System
- **Success States**: Green indicators with checkmarks
- **Warning States**: Yellow indicators with caution icons
- **Error States**: Red indicators with clear error messages
- **Info States**: Blue indicators with helpful information

## 🔒 Security

### API Key Protection
- **Streamlit Secrets**: Secure storage in `.streamlit/secrets.toml`
- **Environment Variables**: Alternative secure storage method
- **No Hardcoding**: Keys never embedded in source code
- **Input Masking**: Password-type fields for manual entry

### Data Privacy
- **Local Processing**: Transcripts processed locally when possible
- **No Data Storage**: User inputs not persisted to disk
- **Session Isolation**: Separate sessions for different users
- **Transparent Operations**: Clear indication of data flow

### Rate Limiting and Quotas
```python
# Built-in rate limiting
RATE_LIMIT_CONFIG = {
    "max_requests_per_minute": 10,
    "cool_down_period": 60,
    "retry_after_header": True
}
```

## 🚀 Deployment

### Streamlit Cloud Deployment
```bash
# 1. Prepare repository
git add .
git commit -m "Deploy to Streamlit Cloud"
git push origin main

# 2. Deploy via Streamlit Cloud
# - Connect GitHub repository
# - Set API keys in secrets
# - Deploy main branch
```

### Self-Hosted Deployment
```bash
# Install system dependencies
sudo apt-get update
sudo apt-get install python3-pip nginx

# Setup application
git clone https://github.com/muhammadawaislaal/youtube-summarizer.git
cd youtube-summarizer

# Create systemd service
sudo nano /etc/systemd/system/youtube-summarizer.service

# Service configuration
[Unit]
Description=YouTube Summarizer Service
After=network.target

[Service]
User=www-data
WorkingDirectory=/var/www/youtube-summarizer
Environment="OPENAI_API_KEY=your_key"
Environment="GROQ_API_KEY=your_key"
ExecStart=/usr/bin/streamlit run app.py --server.port=8501 --server.headless=true
Restart=always

[Install]
WantedBy=multi-user.target

# Enable and start service
sudo systemctl enable youtube-summarizer
sudo systemctl start youtube-summarizer
```

### Docker Compose Deployment
```yaml
version: '3.8'
services:
  youtube-summarizer:
    build: .
    ports:
      - "8501:8501"
    environment:
      - OPENAI_API_KEY=${OPENAI_API_KEY}
      - GROQ_API_KEY=${GROQ_API_KEY}
      - STREAMLIT_SERVER_PORT=8501
      - STREAMLIT_SERVER_ADDRESS=0.0.0.0
    restart: unless-stopped
```

## 🤝 Contributing

### Development Setup
```bash
# Fork and clone repository
git clone https://github.com/your-username/youtube-summarizer.git
cd youtube-summarizer

# Create development branch
git checkout -b feature/new-extraction-method

# Install development dependencies
pip install -r requirements-dev.txt

# Run tests
python -m pytest tests/

# Run development server with hot reload
streamlit run app.py --server.runOnSave true
```

### Contribution Areas
- 🐛 Bug fixes and error handling improvements
- 📺 New transcript extraction methods
- 🤖 Additional AI model integrations
- 🎨 UI/UX enhancements and accessibility
- 📊 Performance optimizations
- 🌐 Multi-language support
- 📚 Documentation improvements

### Code Standards
- Follow PEP 8 style guidelines
- Add type hints for functions
- Include comprehensive docstrings
- Write unit tests for new features
- Update requirements.txt for dependencies
- Use meaningful commit messages

## 📄 License

MIT License

Copyright (c) 2024 YouTube Video Summarizer AI

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## ⚠️ Disclaimer

### YouTube Compliance
- **Terms of Service**: This tool respects YouTube's Terms of Service
- **Public Content**: Only works with publicly available YouTube videos
- **No Bypassing**: Does not bypass any YouTube restrictions or paywalls
- **Educational Use**: Intended for educational and personal use only

### Content Rights
- **Copyright Respect**: Respects content creators' copyrights
- **Fair Use**: Summaries fall under fair use for educational purposes
- **Attribution**: Users should credit original video creators
- **No Commercial Use**: Not for commercial content aggregation

### API Limitations
- **YouTube API**: Does not use official YouTube Data API (rate limits apply)
- **Transcript Availability**: Depends on video having captions available
- **Service Reliability**: Transcript extraction depends on third-party services
- **AI Limitations**: Summaries may contain inaccuracies; verify with original content

## 👨‍💻 Developer

### Project Maintainer
**Muhammad Awais Laal**
- 👨‍💻 Full Stack AI Developer
- 📧 Email: m.awaislaal@gmail.com
- 🔗 GitHub: [@muhammadawaislaal](https://github.com/muhammadawaislaal)
- 💼 LinkedIn: [Muhammad Awais Laal](https://linkedin.com/in/muhammadawaislaal)

### Technical Stack
- **Frontend**: Streamlit, Custom CSS
- **Backend**: Python, Requests, BeautifulSoup
- **AI/ML**: OpenAI GPT-3.5, Groq LLaMA 3.1
- **Web Scraping**: BeautifulSoup, XML parsing
- **Deployment**: Streamlit Cloud, Docker, Nginx

### Support
For technical issues or questions:
1. Check [Issues](https://github.com/muhammadawaislaal/youtube-summarizer/issues)
2. Review documentation and FAQs
3. Email: umtitechsolutions@gmail.com
4. Create detailed bug reports with reproduction steps

<div align="center">

---

### ⭐ Support the Project

If you find this project useful, please give it a star on GitHub!

**Built with ❤️ for Learners and Researchers**

*"Turning long videos into concise knowledge"*

</div>
