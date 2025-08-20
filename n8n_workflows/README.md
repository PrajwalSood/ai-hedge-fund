# AI Hedge Fund - n8n Workflow Collection

This directory contains a complete set of n8n workflows that replicate the functionality of the AI Hedge Fund project. These workflows can be imported directly into the n8n UI and provide a visual, no-code interface for running hedge fund analysis with Ollama as the LLM backend.

## 🚀 Quick Start

1. **Install n8n**: Follow the [official installation guide](https://docs.n8n.io/getting-started/installation/)
2. **Install Ollama**: Download from [ollama.ai](https://ollama.ai) and pull a model (e.g., `ollama pull llama3.1:8b`)
3. **Import Workflows**: In n8n, go to "Workflows" → "Import from file" and select the JSON files
4. **Configure**: Set up your Ollama host and financial data API keys
5. **Run**: Execute workflows via webhooks or manual triggers

## 📊 Available Workflows

### 1. Main Hedge Fund Workflow (`main_hedge_fund_workflow.json`)
**Primary analysis workflow that coordinates all AI analysts**

- **Endpoint**: `POST /webhook/hedge-fund-analyze`
- **Purpose**: Complete stock analysis using multiple AI agents
- **Features**:
  - Multi-agent analysis (Warren Buffett, Charlie Munger, Michael Burry)
  - Risk management integration
  - Portfolio decision making
  - Configurable Ollama integration

**Input Parameters**:
```json
{
  "tickers": "AAPL,MSFT,GOOGL",
  "start_date": "2024-01-01",
  "end_date": "2024-12-01",
  "initial_cash": "100000",
  "margin_requirement": "0.5",
  "selected_analysts": "warren_buffett,charlie_munger,michael_burry",
  "ollama_model": "llama3.1:8b",
  "ollama_host": "http://localhost:11434",
  "show_reasoning": "false"
}
```

### 2. Individual Analyst Workflow (`individual_analyst_workflow.json`)
**Single analyst analysis for detailed stock evaluation**

- **Endpoint**: `POST /webhook/analyst-analyze`
- **Purpose**: Get analysis from a specific investment expert
- **Features**:
  - Warren Buffett value investing analysis
  - Charlie Munger rational thinking approach
  - Michael Burry contrarian analysis
  - Peter Lynch growth analysis

**Input Parameters**:
```json
{
  "analyst_type": "warren_buffett",
  "ticker": "AAPL",
  "start_date": "2024-01-01",
  "end_date": "2024-12-01",
  "ollama_model": "llama3.1:8b",
  "ollama_host": "http://localhost:11434",
  "financial_api_key": "your_api_key"
}
```

### 3. Backtesting Workflow (`backtesting_workflow.json`)
**Historical performance simulation**

- **Endpoint**: `POST /webhook/backtest-run`
- **Purpose**: Test strategies against historical data
- **Features**:
  - Multi-period backtesting
  - Performance metrics calculation
  - Risk-adjusted returns
  - Trade execution simulation

**Input Parameters**:
```json
{
  "tickers": "AAPL,MSFT,GOOGL",
  "start_date": "2024-01-01",
  "end_date": "2024-12-01",
  "initial_capital": "100000",
  "margin_requirement": "0.5",
  "selected_analysts": "warren_buffett,charlie_munger",
  "ollama_model": "llama3.1:8b",
  "rebalance_frequency": "weekly"
}
```

### 4. Data Collection Workflow (`data_collection_workflow.json`)
**Financial data aggregation and processing**

- **Endpoint**: `POST /webhook/data-collect`
- **Purpose**: Gather and process market data
- **Features**:
  - Price data collection
  - Fundamental metrics
  - News sentiment analysis
  - Insider trading data
  - Technical indicators calculation

**Input Parameters**:
```json
{
  "tickers": "AAPL,MSFT,GOOGL",
  "start_date": "2024-01-01",
  "end_date": "2024-12-01",
  "financial_api_key": "your_api_key",
  "data_types": "prices,fundamentals,news,insider_trades"
}
```

### 5. Portfolio & Risk Management Workflow (`portfolio_risk_management_workflow.json`)
**Comprehensive risk analysis and portfolio optimization**

- **Endpoint**: `POST /webhook/portfolio-analyze`
- **Purpose**: Analyze portfolio risk and generate recommendations
- **Features**:
  - Value at Risk (VaR) calculation
  - Portfolio concentration analysis
  - Stress testing
  - Rebalancing recommendations
  - AI-powered risk assessment

**Input Parameters**:
```json
{
  "portfolio": {
    "cash": 50000,
    "positions": {
      "AAPL": {"long": 100, "short": 0}
    }
  },
  "tickers": "AAPL,MSFT,GOOGL",
  "risk_tolerance": "moderate",
  "analysis_date": "2024-12-01",
  "lookback_days": "252",
  "ollama_model": "llama3.1:8b"
}
```

### 6. Ollama Configuration Workflow (`ollama_configuration_workflow.json`)
**Ollama setup and model management**

- **Endpoints**: 
  - `GET /webhook/ollama-status` - Check Ollama status
  - `POST /webhook/ollama-configure` - Configure models
  - `POST /webhook/ollama-test` - Test model performance
- **Purpose**: Manage Ollama integration
- **Features**:
  - Service health checks
  - Model availability verification
  - Performance testing
  - Auto-pull missing models

## 🛠️ Configuration

### Ollama Setup
1. **Install Ollama**: Download from [ollama.ai](https://ollama.ai)
2. **Start Service**: Run `ollama serve` (usually starts automatically)
3. **Pull Models**: `ollama pull llama3.1:8b` (recommended for hedge fund analysis)
4. **Verify**: Check `http://localhost:11434/api/tags`

### Recommended Models
- **llama3.1:8b** - Best balance of performance and speed
- **llama3.1:7b** - Faster, slightly less capable
- **mistral:7b** - Good alternative for analysis
- **codellama:7b** - For technical analysis tasks

### Financial Data API
- Sign up for [Financial Datasets API](https://financialdatasets.ai)
- Get API key and set in workflow parameters
- Alternative: Mock data is used when API key is not provided

## 🚦 Usage Examples

### Run Complete Analysis
```bash
curl -X POST http://localhost:5678/webhook/hedge-fund-analyze \
  -H "Content-Type: application/json" \
  -d '{
    "tickers": "AAPL,TSLA,NVDA",
    "ollama_model": "llama3.1:8b",
    "selected_analysts": "warren_buffett,charlie_munger,michael_burry"
  }'
```

### Check Ollama Status
```bash
curl http://localhost:5678/webhook/ollama-status?ollama_host=http://localhost:11434
```

### Run Backtest
```bash
curl -X POST http://localhost:5678/webhook/backtest-run \
  -H "Content-Type: application/json" \
  -d '{
    "tickers": "SPY,QQQ,IWM",
    "initial_capital": "100000",
    "rebalance_frequency": "monthly"
  }'
```

## 📈 Output Examples

### Main Analysis Output
```json
{
  "timestamp": "2024-12-01T12:00:00Z",
  "portfolio_summary": {
    "total_value": 100000,
    "cash": 50000,
    "total_exposure": 50000
  },
  "decisions": {
    "AAPL": {
      "action": "buy",
      "quantity": 50,
      "confidence": 85,
      "reasoning": "Strong fundamentals and competitive moat"
    }
  },
  "analyst_signals": {
    "warren_buffett": {
      "AAPL": {
        "signal": "bullish",
        "confidence": 90,
        "reasoning": "Excellent business quality..."
      }
    }
  }
}
```

### Risk Analysis Output
```json
{
  "risk_dashboard": {
    "overall_score": 75,
    "health_indicators": {
      "leverage_ok": true,
      "concentration_ok": true,
      "violations_ok": true
    }
  },
  "ai_risk_assessment": {
    "overall_risk_rating": "medium",
    "key_concerns": ["Market volatility", "Concentration risk"],
    "recommendations": ["Diversify holdings", "Reduce leverage"]
  }
}
```

## 🔧 Customization

### Adding New Analysts
1. Duplicate an existing analyst node
2. Modify the prompt with new investment philosophy
3. Update the analyst selection logic
4. Test with sample data

### Modifying Risk Parameters
```javascript
// In Initialize Portfolio Analysis node
const riskParams = {
  conservative: {
    max_position_size: 0.10,
    max_leverage: 1.0
  },
  // Add custom risk profile
  custom: {
    max_position_size: 0.20,
    max_leverage: 1.5
  }
};
```

### Integrating New Data Sources
1. Add HTTP Request node for new API
2. Update data processing logic
3. Modify analyst prompts to use new data
4. Test data quality and availability

## 🐛 Troubleshooting

### Common Issues

**Ollama Connection Failed**
- Check if Ollama service is running: `ps aux | grep ollama`
- Verify port: `curl http://localhost:11434/api/tags`
- Try different host: `http://127.0.0.1:11434`

**Model Not Found**
- Pull model: `ollama pull llama3.1:8b`
- List available: `ollama list`
- Check model name spelling

**Slow Performance**
- Use smaller models (7b instead of 13b)
- Reduce context length in prompts
- Increase system resources

**API Rate Limits**
- Add delays between requests
- Implement retry logic
- Use multiple API keys

### Debug Mode
Enable debug output by setting `show_reasoning: "true"` in requests to see detailed analyst reasoning.

## 🔐 Security Considerations

- **API Keys**: Store securely, never commit to version control
- **Network**: Run Ollama on private network if possible
- **Validation**: Validate all input parameters
- **Rate Limiting**: Implement request throttling
- **Monitoring**: Log all trading decisions for audit

## 📚 Additional Resources

- [n8n Documentation](https://docs.n8n.io)
- [Ollama Documentation](https://github.com/ollama/ollama)
- [Financial Datasets API](https://financialdatasets.ai/docs)
- [Original AI Hedge Fund Project](../README.md)

## 🤝 Contributing

1. Fork the repository
2. Create feature branch
3. Test workflows thoroughly
4. Submit pull request with detailed description
5. Include example usage and outputs

## 📄 License

Same as the main project - see [LICENSE](../LICENSE) file.
