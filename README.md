# app.py
Ksm crypto exchange demo 
import streamlit as st

st.set_page_config(
    page_title="KSM Crypto Exchange",
    page_icon="🚀",
    layout="wide"
)

st.title("🚀 KSM CRYPTO EXCHANGE")
st.subheader("Your Digital Trading Platform")

st.success("Demo Account Active")

# Demo Wallet
if "balance" not in st.session_state:
    st.session_state.balance = 1000.0

if "btc" not in st.session_state:
    st.session_state.btc = 0.0

# Demo Price
BTC_PRICE = 65000.0

st.header("💰 My Wallet")

col1, col2 = st.columns(2)

with col1:
    st.metric("USDT Balance", f"{st.session_state.balance:.2f} USDT")

with col2:
    st.metric("BTC Holdings", f"{st.session_state.btc:.8f} BTC")

st.divider()

st.header("📈 BTC / USDT")

st.metric("Demo BTC Price", "$65,000")

st.header("💱 Demo Trading")

trade_type = st.selectbox(
    "Select Trade",
    ["BUY", "SELL"]
)

amount = st.number_input(
    "Enter Amount (USDT)",
    min_value=1.0,
    value=100.0
)

if st.button("Execute Trade"):

    btc_amount = amount / BTC_PRICE

    if trade_type == "BUY":

        if amount <= st.session_state.balance:
            st.session_state.balance -= amount
            st.session_state.btc += btc_amount
            st.success("BUY Order Successful!")

        else:
            st.error("Insufficient USDT Balance!")

    elif trade_type == "SELL":

        if btc_amount <= st.session_state.btc:
            st.session_state.btc -= btc_amount
            st.session_state.balance += amount
            st.success("SELL Order Successful!")

        else:
            st.error("Insufficient BTC Balance!")

st.divider()

st.header("📋 Exchange Information")

st.write("✅ Demo Trading")
st.write("✅ BTC / USDT Market")
st.write("✅ Demo Wallet")
st.write("✅ BUY / SELL System")

st.warning(
    "This is an educational demo. No real money or live trading is supported."
)

st.caption("© 2026 KSM Crypto Exchange")
