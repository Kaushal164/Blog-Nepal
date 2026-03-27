# 📰 Professional News & Media Blog

A modern, professional Django-based blog application for publishing news articles and managing content. Perfect for individuals, news organizations, or media companies looking to share stories with their audience.

**Built from Nepal 🇳🇵 | Created with love for quality journalism**

![Python](https://img.shields.io/badge/Python-3.8+-blue)
![Django](https://img.shields.io/badge/Django-3.0+-green)
![Database](https://img.shields.io/badge/Database-SQLite-lightblue)
![License](https://img.shields.io/badge/License-MIT-yellow)
![Status](https://img.shields.io/badge/Status-Production%20Ready-brightgreen)

## ✨ What Can You Do With This?

- ✍️ **Publish Articles** - Create and manage news articles with a simple admin panel
- 📱 **Mobile Friendly** - Works perfectly on phones, tablets, and computers
- 💬 **Contact Your Readers** - Built-in contact form for reader inquiries
- 🎨 **Professional Look** - Modern design with smooth animations and gradients
- 📅 **Auto Timestamps** - Every article is automatically dated when published
- 🌍 **About Your Site** - Dedicated About section to tell your story
- ⚡ **Fast Loading** - Optimized for quick performance
- 🎯 **Article Previews** - Show snippets of articles on the homepage

## � What You Need Before Starting

1. **Python 3.8+** - [Download Python](https://www.python.org/downloads/)
2. **A Code Editor** - VS Code, PyCharm, or any text editor
3. **Terminal/Command Prompt** - To run commands
4. **Internet Connection** - To download Django

That's it! No complex setup required.

## 🚀 Quick Start (5 Minutes)

### Step 1: Download & Setup
```bash
# Download the project
git clone https://github.com/yourusername/blog.git
cd blog
cd blog
```

### Step 2: Create Virtual Environment (Isolates your project)
**On Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**On Mac/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Django
```bash
pip install django
```

### Step 4: Setup Database
```bash
python manage.py migrate
```

### Step 5: Create Admin Account (To manage your blog)
```bash
python manage.py createsuperuser
```
Follow the prompts:
- Username: (choose something like "admin")
- Email: (your email)
- Password: (create a strong password)

### Step 6: Start Your Blog
```bash
python manage.py runserver
```

Your blog is now running! Open your browser and go to:
- **Homepage**: `http://127.0.0.1:8000/`
- **Admin Panel**: `http://127.0.0.1:8000/admin/`

## � How to Use Your Blog

### Reading the Blog (Public Site)
1. Go to `http://127.0.0.1:8000/`
2. See all your articles on the homepage
3. Click **"Read More →"** to read full article
4. Scroll down to find **About Us** and **Contact** sections

### Publishing Your First Article (Admin Panel)

1. Open `http://127.0.0.1:8000/admin/`
2. Login with your admin account
3. Click **"Posts"** in the left menu
4. Click **"Add Post"** button
5. Fill in:
   - **Title**: Your article headline
   - **Body**: Your article content (can be very long)
   - Date will be added automatically
6. Click **"Save"**
7. Your article now appears on the homepage!
� Understanding the Project Structure

```
blog/                          # Main project folder
│
├── blog/                       # Django configuration
│   ├── settings.py            # Project settings (don't change much)
│   ├── urls.py                # Main routes
│   └── wsgi.py                # Production settings
│
├── posts/                      # Blog app (where articles are stored)
│   ├── models.py              # Database structure for articles
│   ├── views.py               # Logic to display articles
│   ├── urls.py                # Routes for blog
│   ├── admin.py               # Admin panel setup
│   └── migrations/            # Database changes
│
├── templates/                  # HTML pages
│   ├── Index.html             # Homepage template
│   └── posts.html             # Single article page template
│
├── db.sqlite3                 # Database file (stores all articles)
├── manage.py                  # Command center for Django
└── README.md                  # This file
```

## 📊 How Articles Are Stored

Each article has:
- **Title** - The headline (max 100 characters)
- **Body** - Full article content (almost unlimited)
- **Created At** - Date & time (automatically set) Post Model
```python
class Post(models.Model):
    title = CharField(max_length=100)           # Article title
    body = CharField(max_length=1000000)        # Article content
    created_at = DateTimeField()                # Publication date & time
```

## 🌐 URL Patterns

| URL | Purpose |
|-----|---------|
| `/` | Home page - displays all articles |
| `/post/<id>/` | Single article view |
| `/adWebsite Pages

| Page | Link | What You See |
|------|------|-------------|
| Homepage | `/` | All articles with previews |
| Single Article | `/post/1/`, `/post/2/` | Full article content |
| Admin Panel | `/admin/` | Create/Edit/Delete articles |

## 💻 Technical Details & Code Structure

### 1. Article Model (How Articles Are Stored)

**File: `posts/models.py`**
```python
from django.db import models
from datetime import datetime

class Post(models.Model):
    title = models.CharField(max_length=100)           # Article headline
    body = models.CharField(max_length=1000000)        # Article content
    created_at = models.DateTimeField(default=datetime.now, blank=True)

    def __str__(self):
        return self.title

    class Meta:
        ordering = ['-created_at']  # Newest articles first
```

### 2. Views (How Articles Are Displayed)

**File: `posts/views.py`**
```python
from django.shortcuts import render
from .models import Post

def Index(request):
    posts = Post.objects.all()  # Get ALL articles
    return render(request, 'Index.html', {'posts': posts})

def post(request, pk):
    posts = Post.objects.get(id=pk)  # Get ONE article by ID
    return render(request, 'posts.html', {'posts': posts})
```

### 3. URL Routing

**File: `posts/urls.py`**
```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.Index, name='Index'),  # Homepage
    path('post/<str:pk>/', views.post, name='post'),  # Single article
]
```

### 4. Template Usage

**File: `templates/Index.html`**
```html
{% for post in posts reversed %}
<div class="post">
    <a href="/post/{{post.id}}/">
        <h2>{{ post.title }}</h2>
        <p>{{ post.body|truncatewords:50 }}</p>
    </a>
</div>
{% endfor %}
```

### 5. Database Queries

```python
from posts.models import Post

# Get all posts
posts = Post.objects.all()

# Get one post
post = Post.objects.get(id=1)

# Create post
Post.objects.create(title="Title", body="Content")

# Update post
post.title = "New Title"
post.save()

# Delete post
Post.objects.get(id=1).delete()
```

### 6. Admin Setup

**File: `posts/admin.py`**
```python
from django.contrib import admin
from .models import Post

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ('title', 'created_at')
    search_fields = ('title', 'body')
    list_filter = ('created_at',)
```

## 🌐 Website Pages

| Page | Link | What You See |
|------|------|-------------|
| Homepage | `/` | All articles with previews |
| Single Article | `/post/1/`, `/post/2/` | Full article content |
| Admin Panel | `/admin/` | Create/Edit/Delete articles |

## 🎨 Easy Customization

### Change Your Blog Colors

Open `templates/Index.html` and find the colors in the `<style>` tag:
```css
/* Change these colors */
#0284c7  /* Primary Blue - buttons, headers */
#0369a1  /* Secondary Blue - accents */
#f0f9ff  /* Light Blue - background */
```

### Update Your Contact Info

In `templates/Index.html`, find the Contact section and edit:
```html
<p><a href="mailto:info@professionalblog.com">info@professionalblog.com</a></p>
<p><a href="tel:+977-1-234-5678">+977-1-234-5678</a></p>
<p>Kathmandu, Nepal</p>
```

### Write Your About Section

In `templates/Index.html`, find "About Us" section and replace with your content:
```html
<p>Your blog description here...</p>
```🆘 Troubleshooting

### "Command not found: python"
- Make sure Python is installed: `python --version`
- On Mac, use `python3` instead of `python`

### "ModuleNotFoundError: No module named 'django'"
- M🚀 Deploy Online (Make It Live)

### Option 1: Heroku (Easiest for Beginners)
1. Create account at [heroku.com](https://www.heroku.com)
2. Install Heroku CLI
3. Create file `Procfile`:
   ```
   web: gunicorn blog.wsgi
   ```
4. Create `requirements.txt`:
   ```bash
   pip freeze > requirements.txt
   ```
5. Deploy:
   ```bash
   heroku login
   heroku create your-app-name
   git push heroku main
   ```

### Option 2: PythonAnywhere
1. Go to [pythonanywhere.com](https://www.pythonanywhere.com)
2. Sign up for free account
3. Upload your project files
4. Configure WSGI file
5. Visit your live URL

### Option 3: DigitalOcean / AWS / Google Cloud
Requires more technical knowledge. See their Django deployment guides.

## 📚 Learn More

- **Django Beginners**: https://docs.djangoproject.com/
- **Python**: https://python.org
- **HTML/CSS**: https://w3schools.com

## 🆘 Help & Support

**Got stuck?**
1. Check the Troubleshooting section above
2. Read Django official docs
3. Search on Stack Overflow
4. Create a GitHub issue

**Have ideas?**
- Create a Pull Request with improvements
- Open an Issue with your suggestions

## 🎯 Next Steps

1. ✅ Get the project running locally
2. ✅ Create your first article
3. ✅ Customize colors and text
4. ✅ Deploy online
5. ✅ Share with the world!

## 📝 License

MIT License - Use this project however you want!

## 👨‍💻 Credits

Created in Nepal 🇳🇵 for quality journalism

---

### Quick Command Reference

```bash
# Activate virtual environment (Windows)
venv\Scripts\activate

# Activate virtual environment (Mac/Linux)
source venv/bin/activate

# Install dependencies
pip install django

# Setup database
python manage.py migrate

# Create admin account
python manage.py createsuperuser

# Start server
python manage.py runserver

# Stop server
Ctrl + C

# Deactivate virtual environment
deactivate
```

---

**⭐ Star this project if it helped you! Happy blogging! 🚀**
- Django framework for excellent documentation
- Google Fonts for Poppins typeface
- The open-source community for inspiration

## 📅 Changelog

### Version 1.0.0 (2026-03-26)
- Initial release
- Core blog functionality
- Professional UI design
- About and Contact sections
- Responsive design for all devices

---

**Made with ❤️ from Nepal**

⭐ If you find this project useful, please consider giving it a star on GitHub!
