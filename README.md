BoolSpark ⚡
AI-Powered Boolean Search String Generator for Recruiters

BoolSpark transforms job descriptions into optimized Boolean search strings in seconds, not minutes. Upload a job description (PDF/DOCX), and let AI craft professional search strings for sourcing candidates on LinkedIn, Google, and other platforms.

🌟 Features
Core Functionality
AI-Powered Generation: Leverages DeepSeek API to analyze job descriptions and create intelligent Boolean strings
Multi-Level Output: Generates Basic, Advanced, and LinkedIn X-Ray search strings
File Upload Support: Accepts PDF and DOCX formats (up to 10MB)
Instant Refresh: Regenerate new variations with a single click
AI Insights: Get explanations of the search strategy and keyword choices
Productivity Tools
Copy to Clipboard: One-click copy for all boolean strings
Download as TXT: Export formatted boolean strings for offline use
Shareable Links: Generate unique URLs to share boolean strings with your team
View Tracking: Monitor how many times shared links have been viewed
History Management: Access and reuse previously generated strings
Advanced Features
Batch Processing: Upload and process multiple job descriptions at once
Custom Formatting: Adjust operators (AND/OR), quote styles, and case preferences
Analytics Dashboard: Track usage patterns, popular skills, and file type breakdown
Dark Mode: Full theme support with light, dark, and system modes
Responsive Design: Works seamlessly on desktop, tablet, and mobile devices
🚀 Quick Start
Prerequisites
Node.js 18+ installed
PostgreSQL database (Neon recommended)
DeepSeek API key (Get one here)
Installation
Clone and install dependencies

npm install

Set up environment variables

Create a .env file with the following:

DATABASE_URL=postgresql://user:password@host:5432/database
DEEPSEEK_API_KEY=sk-your-deepseek-api-key
SESSION_SECRET=your-random-secret-string

Initialize the database

npm run db:push

Start the development server

npm run dev

Open your browser

Navigate to http://localhost:5000

📖 Usage Guide
Generating Boolean Strings
Upload a Job Description

Drag and drop a PDF or DOCX file
Or click to browse and select a file
Generate

Click "Generate Boolean String"
Wait for AI to analyze the job description (typically 15-20 seconds)
Use Your Results

Basic Boolean: Simple OR-based keyword search
Advanced Boolean: Complex query with AND/OR logic
LinkedIn X-Ray: Optimized for LinkedIn profile searches
Refresh for Variations

Click the refresh icon to generate alternative boolean strings
Each refresh creates a new variation with different keyword combinations
Sharing & Collaboration
Create a Share Link

Click the Share button (chain icon)
Choose expiration period (optional)
Copy the generated URL
Track Engagement

View count updates automatically
Monitor which searches are most popular
Customization Options
Access settings to customize:

Operators: Change AND/OR to symbols (&, |, +, etc.)
Quote Style: Double quotes, single quotes, or none
Parentheses: Round, square, curly, or none
Case: UPPERCASE, lowercase, or preserve original
🏗️ Tech Stack
Frontend
React 18 with TypeScript
Vite for blazing-fast builds
TanStack Query (React Query) for data fetching
Wouter for routing
Shadcn/ui component library
Tailwind CSS for styling
Lucide React for icons
Backend
Express.js server
PostgreSQL database (Neon serverless)
Drizzle ORM for type-safe queries
pdf-parse for PDF processing
mammoth for DOCX processing
DeepSeek API for AI generation
🔧 API Reference
POST /api/generate-boolean
Generate boolean strings from job description text.

Request Body:

{
  "text": "Job description text...",
  "apiKey": "sk-optional-api-key",
  "fileName": "optional-file-name.pdf",
  "regenerate": false
}

Response:

{
  "basic": "Recruiter OR Talent OR HR",
  "advanced": "(Recruiter OR \"Talent Acquisition\") AND (LinkedIn OR Sourcing)",
  "linkedin": "site:linkedin.com/in/ (Recruiter OR \"Talent Acquisition\")",
  "insights": "Strategy explanation...",
  "id": 123
}

GET /api/history
Retrieve generation history.

Query Parameters:

limit (optional): Number of items to return (default: 50)
POST /api/share
Create a shareable link.

Request Body:

{
  "booleanStringId": 123,
  "expiresInDays": 30
}

GET /api/analytics/overview
Get usage statistics.

Response:

{
  "totalGenerations": 245,
  "totalSharedLinks": 18,
  "totalViews": 127,
  "avgGenerationsPerDay": 12.3
}

🎨 Design System
BoolSpark uses a modern, professional design with:

Primary Color: Purple (#7C3AED) - Brand identity and CTAs
Secondary Color: Cyan (#06B6D4) - Accents and highlights
Typography: Inter for UI, JetBrains Mono for code/boolean strings
Spacing: Consistent 4px-based spacing system
Dark Mode: Full support with optimized colors for readability
🔐 Environment Variables
Variable	Description	Required
DATABASE_URL	PostgreSQL connection string	Yes
DEEPSEEK_API_KEY	DeepSeek API key for AI generation	Yes
SESSION_SECRET	Secret for session encryption	Yes
PGHOST	PostgreSQL host	Auto-set by Replit
PGPORT	PostgreSQL port	Auto-set by Replit
PGUSER	PostgreSQL username	Auto-set by Replit
PGPASSWORD	PostgreSQL password	Auto-set by Replit
PGDATABASE	PostgreSQL database name	Auto-set by Replit
📊 Database Schema
boolean_strings
Stores generated boolean search strings.

{
  id: number (primary key)
  jobTitle: string
  jobDescription: text
  basic: text
  advanced: text
  linkedin: text
  insights: text
  fileName: string
  createdAt: timestamp
}

shared_links
Manages shareable links and view tracking.

{
  id: number (primary key)
  booleanStringId: number (foreign key)
  shareSlug: string (unique)
  viewCount: number
  expiresAt: timestamp
  createdAt: timestamp
}

analytics_events
Tracks usage events for analytics.

{
  id: number (primary key)
  eventType: string
  booleanStringId: number (foreign key)
  metadata: jsonb
  createdAt: timestamp
}

🐛 Known Issues & Solutions
Boolean Strings Truncated
Fixed in v1.1.0 - Increased DeepSeek max_tokens from 1000 to 3000 and improved regex parsing for escaped quotes.

Refresh Returns Same String
This is expected behavior. The AI produces consistent results for the same input. The refresh feature uses higher temperature (0.7 vs 0.3) to create variations, but results may still be similar for highly specific job descriptions.

Dark Mode Text Visibility
Fixed - BoolSpark title now uses solid purple color instead of gradient for reliable cross-browser visibility.

🚢 Deployment
BoolSpark is optimized for deployment on Replit:

Push Code to Repository

git push origin main

Configure Secrets

Add DEEPSEEK_API_KEY in Replit Secrets
Database variables are auto-configured
Deploy

Click "Deploy" in Replit
Your app will be live at your-repl.replit.app
For other platforms (Vercel, Railway, Render):

Ensure PostgreSQL database is provisioned
Set all environment variables
Build command: npm run build
Start command: npm start
🤝 Contributing
We welcome contributions! Here's how to get started:

Fork the repository
Create a feature branch (git checkout -b feature/amazing-feature)
Commit your changes (git commit -m 'Add amazing feature')
Push to the branch (git push origin feature/amazing-feature)
Open a Pull Request
📝 License
This project is proprietary software. All rights reserved.

🙏 Acknowledgments
DeepSeek for powering the AI generation
Neon for serverless PostgreSQL
Shadcn/ui for beautiful components
Replit for hosting and development platform
📧 Support
For questions, issues, or feedback:

Open an issue on GitHub
Contact the development team
Check the documentation
Built with ❤️ for recruiters who value efficiency
