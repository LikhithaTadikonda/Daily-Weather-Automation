# Daily Weather Automation 

## API Setup & Key Configuration

### OpenWeatherMap API

1. **Sign up**: Visit https://openweathermap.org/api
2. **Get API Key**:
   - Navigate to https://home.openweathermap.org/api_keys
   - Your API key: `723cdf3da2922631843579df25b13f7f`
   - Status: Active
3. ** Activation Time**: New API keys take 1-2 hours to activate
4. **Test API Key** (after activation):
https://api.openweathermap.org/data/2.5/weather?q=London&appid=723cdf3da2922631843579df25b13f7f&units=metric


### Configure in n8n:
- Open **HTTP Request** node
- Update URL format:

https://api.openweathermap.org/data/2.5/weather?q=YOUR_CITY&appid=YOUR_API_KEY&units=metric

- Replace `YOUR_CITY` with desired location
- Replace `YOUR_API_KEY` with your OpenWeatherMap key

---

##  Supabase Database Configuration

### Project Information
- **Project Name**: weather-app
- **Organization**: LikhithaTadikonda's Org (FREE tier)
- **Project URL**: `https://favajsiomwxywvusoaob.supabase.co`
- **Region**: Americas

### Database Schema

**Table Name**: `weather_logs`

### Supabase API Credentials

**For n8n Configuration:**
- **Host**: `https://favajsiomwxywvusoaob.supabase.co`
- **API Key (anon public)**: 

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImZhdmFqc2lvbXd4eXd2dXNvYW9iIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NjYxNzM4NzMsImV4cCI6MjA4MTc0OTg3M30.h63vqy1nGFF_D-z3ArQtXL5312mZ6LMDXTObOZd7Ogw

### Setup in n8n:
1. Open **Create a row** (Supabase) node
2. Click **Select Credential** → **Create New Credential**
3. Enter credentials:
 - **Host**: Project URL above
 - **Service Role Secret**: API Key above
4. Click **Save**
5. Select **Table**: `weather_logs`
6. Select **Operation**: `Create`

---

##  Email Configuration (Gmail SMTP)

### Gmail SMTP Settings

- **Email Address**: `likhithatadikonda19@gmail.com`
- **SMTP Host**: `smtp.gmail.com`
- **Port**: `465`
- **SSL/TLS**: Enabled ✓
- **Authentication**: Required
- **Password**: App-specific password (generated above)

### Configure in n8n:

1. Open **Send email** node
2. Click **Select Credential** → **Create New Credential**
3. Fill in SMTP details:
 - **User**: your-email@gmail.com
 - **Password**: 16-character app password
 - **Host**: smtp.gmail.com
 - **Port**: 465
 - **SSL/TLS**: Toggle ON
4. Click **Save**
5. Update email fields in node:
 - **From Email**: likhithatadikonda19@gmail.com
 - **To Email**: likhithatadikonda19@gmail.com (or recipient email)
 - **Subject**: `Daily Weather for {{ $json.city }} - {{ $now.format('YYYY-MM-DD') }}`

---

## How to Import & Run the Workflow

### Import Workflow to n8n

1. **Download Workflow**:
 - In n8n, click the **≡** menu (top right)
 - Select **Download** to get the JSON file

2. **Import to New n8n Instance**:
 - Go to n8n dashboard
 - Click **Workflows** → **Add Workflow**
 - Click **Import from File**
 - Upload the downloaded JSON file


After importing, configure these nodes:

#### 1. HTTP Request Node
- Update URL with your API key and city
- Example: `https://api.openweathermap.org/data/2.5/weather?q=London&appid=YOUR_KEY&units=metric`

#### 2. Supabase Node
- Add Supabase credentials
- Select `weather_logs` table
- Ensure operation is set to `Create`

#### 3. Send Email Node
- Add Gmail SMTP credentials
- Update From/To email addresses
- Customize subject line if needed
