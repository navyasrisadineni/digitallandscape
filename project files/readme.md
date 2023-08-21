import requests
from bs4 import BeautifulSoup
from collections import Counter
import matplotlib.pyplot as plt

# Function to scrape a webpage and extract its text content
def scrape_webpage(url):
    response = requests.get(url)
    if response.status_code == 200:
        soup = BeautifulSoup(response.text, 'html.parser')
        text_content = soup.get_text()
        return text_content
    else:
        print(f"Failed to retrieve content from {url}")
        return None

# Function to analyze word frequency in text
def analyze_word_frequency(text_content):
    words = text_content.lower().split()
    word_count = Counter(words)
    return word_count

# Function to plot word frequency
def plot_word_frequency(word_count, num_words=10):
    common_words = word_count.most_common(num_words)
    words, counts = zip(*common_words)
    
    plt.figure(figsize=(10, 6))
    plt.bar(words, counts)
    plt.title('Top Words in Webpage')
    plt.xlabel('Words')
    plt.ylabel('Frequency')
    plt.xticks(rotation=45)
    plt.tight_layout()
    plt.show()

if __name__ == "__main__":
    # Replace this with the URL of the webpage you want to analyze
    target_url = "https://example.com"
    
    # Scrape webpage and extract text content
    webpage_content = scrape_webpage(target_url)
    
    if webpage_content:
        # Analyze word frequency
        word_count = analyze_word_frequency(webpage_content)
        
        # Plot word frequency
        plot_word_frequency(word_count)
    else:
        print("Analysis failed due to missing webpage content.")

