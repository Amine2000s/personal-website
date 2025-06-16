# 🧠 The Bac Exam Is Here… So I Built a Web Scraper
*When the government cuts the internet, you cut through HTML instead.*


![sad deeveloper](../assets/images/blog/sad-algerian-developer.jpg)


imagine this . 

You're grinding through your online learning marathon — Spring Boot, Maven, Servlets, maybe even a cheeky "Data Structures" refresher on the side. You’re cruising through MaharaTech like a boss. Then suddenly...

💥 **BREAKING NEWS:**

> “The internet will be shut down nationwide for 5 days.”
> 

Yep. Welcome to Algeria during the *Baccalauréat* exams. To stop cheating, they disconnect the entire country from the web.

And I'm like:

> “Bro… I got like four online courses going on. 😭”
> 

My options?

1. Sit in offline darkness.
2. Magically teleport myself to another country.
3. **Web. Scrape. Everything.**

You already know what I chose.

I built a web scraper that crawled every course, hunted down every lesson, cracked open MaharaTech's sidebar structure, and **ripped out embedded YouTube links like a digital archaeologist with a mission.**

This blog is the story of that ridiculous journey.

It’s Web Scraping 101, but with chaos, deadlines, debugging rage, and some solid laughs.

---

## 🎯 What You’ll Learn in This Blog

- How to navigate a login system that uses Google OAuth2
- How to use Playwright (like Selenium, but better and sexier)
- How to programmatically extract YouTube video links hiding inside complex iframes
- How to save entire course structures — chapters, videos, links — before they vanish
- How to not lose your mind while doing all this under extreme pressure

---

## ✨ Chapter 1: Inspecting the Battlefield (MaharaTech)

The first thing I did was open MaharaTech in the browser and stare at the course page like a detective at a crime scene.

MaharaTech organizes content into a sidebar tree. Each chapter is a collapsible section, and each section hides multiple video lessons embedded in an iframe. Not just any iframe, though — *a YouTube iframe wrapped in a playful cloak of JavaScript invisibility*.

Not fun.

So, I opened DevTools and asked myself:

> "Where do the links live? How is the DOM structured? Is it dynamically injected?"
> 

The answer: yes, yes, and **YES**. Which means we needed a headless browser capable of waiting, clicking, and extracting content *after* the page has finished rendering all its JS magic.

---

## ⚖️ Chapter 2: Why Playwright > Selenium

I started with Selenium. It was fine. Until it wasn’t.

OAuth2 logins with Google? Pain.

Waiting for lazy-loaded elements to show up? Pain.

Switching frames and extracting content? *Excruciating pain.*

So I switched to **Playwright**. And it felt like upgrading from a horse cart to a Tesla.

With Playwright:

- You can launch a persistent browser session with your own profile
- You can inject cookies directly (hello, bypassing Google login)
- Frame management is way smoother

And my favorite: it has a synchronous API. No `async/await hell`.

---

## 🌐 Chapter 3: Logging In with Cookies

Logging in to MaharaTech was blocked behind Google OAuth. Trying to do it programmatically gets you a big fat error:

> “This browser or app may not be secure.”
> 

So I took a detour:

I logged in **manually** in my real browser, copied my MaharaTech cookies, and injected them into the Playwright session.

```python
context.add_cookies(convert_cookie_string_to_playwright(cookie_string))

```

And like magic: I was authenticated, and MaharaTech loaded perfectly.

---

## 👀 Chapter 4: Scraping All Sections and Lessons

Now came the fun part: crawling the DOM to extract all the section titles, and their lesson links.

I inspected the HTML and found that the sidebar had an ID of `#courseindex-content`. Inside it? Divs representing each chapter.

Each video lesson? A `li` tag with an ID starting with `course-index-cm-`, and a `href` pointing to `mod/hvp/view.php?id=...`.

So I wrote a Playwright + BeautifulSoup hybrid:

- Go to the course page
- Wait until sidebar loads
- Loop through all sidebar chapters
- For each chapter, collect all lessons
- Save everything in a `.txt` file, line by line

---

## 🎞️ Chapter 5: Extracting YouTube Links from Lesson Pages

Every lesson page had an embedded YouTube iframe.

But the catch? Not all loaded instantly. Some took 5–10 seconds.

So I built a retry system:

```python
for attempt in range(5):
    page.evaluate("window.scrollBy(0, 9999)")
    time.sleep(3)
    for frame in page.frames:
        if "youtube.com" in frame.url:
            yt_url = frame.url
            break

```

After detecting the `embed/VIDEO_ID`, I cleaned it to standard `watch?v=VIDEO_ID` format.

Boom. Now we had direct YouTube links for every lesson.

---

## 📁 Chapter 6: Saving Everything to Disk

Each step saved structured output to text files:

- `course_structure.txt` for chapters and lessons
- `youtube_links.txt` for cleaned YouTube URLs

That way, even when the internet goes dark, I can:

- Watch everything offline via `yt-dlp` or similar
- Review lesson names and order
- Sleep soundly knowing I outsmarted the Bac shutdown

---

## ✨ Bonus: Why This Was Worth It

Yes, I could have just screen-recorded. Or asked a friend to send videos.

But this little project taught me:

- Real-world use of Playwright
- HTML/DOM traversal
- Dealing with iframes, cookies, and scraping under pressure
- That pain + pressure = motivation to finish fast

And honestly? I had fun.

Now when someone asks me: "Why did you build a web scraper?"

> I say: "Because the government turned off the internet, and I had learning to do."
> 

---

## 📆 Coming Soon

- How to download scraped YouTube links via `yt-dlp`
- Turning this scraper into a GUI app
- Packaging it into a plug-n-play template for others

---

**TL;DR:**

Web scraping isn't just about code. It's about *survival*, *ingenuity*, and getting your content *before the internet ghosts you*.

Thanks for reading. And if you're reading this during Bac week?

> May your courses be backed up, and your bandwidth be fast. ✅
>