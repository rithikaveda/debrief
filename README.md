Debrief
A personalized daily news briefing system powered by Claude Code. It searches the web for the last 24 hours of news across 7 topics, generates a concise briefing, and emails it to you every morning.

How It Works
generate.sh runs Claude Code in non-interactive mode (claude -p) with web search enabled
Claude searches 100+ curated sources across geopolitics, tech, AI, India, markets, culture, and health
The briefing is saved as a markdown file in briefings/
email_briefing.py sends it as a styled HTML email via Gmail SMTP
Project Structure
debrief/
├── generate.sh          # Main script — generates briefing and optionally emails it
├── email_briefing.py    # Sends the briefing via Gmail SMTP
├── prompt.md            # The prompt that drives briefing generation
├── sources.md           # Full database of 100+ curated news sources
├── briefings/           # Generated briefings (one per day)
│   └── briefing-YYYY-MM-DD.md
└── cron.log             # Cron job output log
Setup
Prerequisites
Claude Code CLI installed and authenticated
Python 3
A Gmail account with an App Password
Environment Variables
Add these to your ~/.zshrc or ~/.bashrc:

export BRIEFING_EMAIL='your.email@gmail.com'
export GMAIL_APP_PASSWORD='your-16-char-app-password'
Run Manually
# Generate briefing only
./generate.sh

# Generate and email
./generate.sh --email
Schedule Daily (cron)
To receive the briefing at 6 AM every day:

crontab -e
# Add this line:
0 6 * * * source ~/.zshrc && /path/to/debrief/generate.sh --email >> /path/to/debrief/cron.log 2>&1
Note: Cron only runs when your machine is awake. On macOS, consider using launchd for wake-resilient scheduling.

Topics Covered
#	Topic	Example Sources
1	Global Geopolitics	Geopolitical Futures, Peter Zeihan, CSIS, The Diplomat
2	Tech & Startups	TechCrunch, Stratechery, TLDR Tech, Lenny's Newsletter
3	AI Developments	Import AI, The Batch, Ben's Bites, Superhuman AI
4	India Politics & Startups	Inc42, The Morning Context, The Ken, YourStory
5	Markets & Portfolio Signals	Money Stuff, Axios Markets, The Diff, Doomberg
6	Culture, Media & Discourse	The Rebooting, ICYMI, Link In Bio, Marketing Brew
7	Longevity & Health	Peter Attia, GLP-1 Digest, Health Tech Nerds
Customization
Edit prompt.md to change topics, tone, sources, or format
Edit sources.md to update the full source database
The email template in email_briefing.py can be restyled as needed
License
MIT
