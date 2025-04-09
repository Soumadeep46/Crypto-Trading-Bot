# Crypto Trading Bot


This is an advanced AI-powered trading bot developed for the  KodeKurrent Hackathon. Our bot implements multiple sophisticated trading strategies to optimize performance across various market conditions, with a focus on risk management and consistent returns.

## 👥 Team Blazin

- **Team Leader:** Soumadeep Samanta  
- **Team Members:** Aditya Bhattacharya, Arnav Yadav

---

## 📊 Trading Strategies

Our trading bot combines several advanced strategies to adapt to different market conditions:

### 1. Momentum Trading

Captures market trends by trading in the direction of price movements using:

- Moving Averages (SMA and EMA)
- Relative Strength Index (RSI)

### 2. Grid Trading

Profits from price fluctuations in range-bound markets by:

- Placing buy and sell orders at predetermined intervals
- Automatically executing trades when price hits grid levels

### 3. DCA (Dollar Cost Averaging) Trading

Captures large, long-term trends by leveraging:

- Moving average crossovers (Golden Cross and Death Cross)
- Dynamic position sizing based on trend strength

### 4. 30-70 RIS Trading Strategy

Optimizes risk-to-reward ratios with:

- Fixed 30% risk / 70% reward ratio per trade
- Statistical modeling for trade execution

### 5. Sharpe Ratio Optimization

Improves risk-adjusted returns through:

- Algorithmic performance tuning
- Machine learning for parameter optimization

---

## 🛠️ Installation & Setup

### Prerequisites

- Python 3.8 or higher  
- Node.js 14 or higher (for web dashboard)

### Step 1: Clone the Repository

```bash
git clone https://github.com/Soumadeep46/Crypto-Trading-Bot
```

## Step 2: Install Python Dependencies

```bash
pip install numpy pandas matplotlib mplfinance requests hmac hashlib logging datetime
```

## Step 3: Install Node.js Dependencies (for Web Dashboard)

```bash
npm install express socket.io chart.js react react-dom next tailwindcss
```

## Step 4: Configure API Keys
Create a .env file in the root directory with your API keys:
```env
API_KEY=your_api_key_here
SECRET_KEY=your_secret_key_here
API_BASE_URL=https://api.exchange.com
```

## 🚀 Running the Bot
### Running the Grid Trading Strategy

```bash
python grid.py
```

### Running the DCA Trading Strategy

```bash
python dca.py
```

### Running the Momentum Trading Strategy

```bash
python momentum.py
```

### Running the Web Dashboard

```bash
npm run dev
```

Then open your browser to http://localhost:3000


## 📈 Performance Analysis
Our bot demonstrated strong performance during testing:

- Consistent Returns: Stable returns with low drawdowns

- Effective Risk Management: Optimized risk-to-reward ratios

- Adaptability: Performed well across various market conditions



## 🧠 Technical Implementation
### Grid Strategy Implementation
The grid strategy places buy and sell orders at predetermined intervals around the current market price:

```python
def create_grid_orders(self):
    for i in range(1, self.grid_size + 1):
        self.buy_orders.append(self.current_price - i * self.grid_interval)
        self.sell_orders.append(self.current_price + i * self.grid_interval)
```

### RSI Calculation
The RSI indicator helps identify overbought and oversold conditions:

```python
def calculate_rsi(self, data):
    delta = data['price'].diff().dropna()
    gain = (delta.where(delta > 0, 0)).rolling(window=self.rsi_period).mean()
    loss = (-delta.where(delta < 0, 0)).rolling(window=self.rsi_period).mean()
    rs = gain / loss
    rsi = 100 - (100 / (1 + rs))
    return rsi.iloc[-1]
```

### Moving Average Crossover
The DCA strategy uses moving average crossovers to identify trends:

```python
def dynamic_cross_signal(short_term_ma, long_term_ma):
    if short_term_ma[-1] > long_term_ma[-1] and short_term_ma[-2] < long_term_ma[-2]:
        return 'BUY'
    elif short_term_ma[-1] < long_term_ma[-1] and short_term_ma[-2] > long_term_ma[-2]:
        return 'SELL'
    else:
        return 'HOLD'
```

## 📝 API Documentation

### RoostooAPIClient

The main API client class handles all communication with the exchange:

- `get_ticker(pair)`: Fetches current price data  
- `place_order(pair, side, order_type, quantity, price)`: Places a trade order  
- `_sign(params)`: Signs API requests for authentication

## 🔒 Security Considerations

- API keys are stored in environment variables, not hardcoded  
- HMAC SHA-256 authentication is used for API requests  
- Rate limiting is implemented to avoid API restrictions  

---
