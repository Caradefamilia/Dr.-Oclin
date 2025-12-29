import streamlit as st
import pandas as pd

st.set_page_config(page_title="Gestão de Ótica", layout="wide")

st.title("👓 Sistema de Controle de Ótica")

# Inicializar banco de dados simples (na memória da sessão)
if 'vendas_otica' not in st.session_state:
    st.session_state.vendas_otica = pd.DataFrame(columns=[
        'Cliente', 'Data', 'OD_Esferico', 'OD_Cilindrico', 'OD_Eixo', 
        'OE_Esferico', 'OE_Cilindrico', 'OE_Eixo', 'Valor'
    ])

# --- CADASTRO ---
with st.expander("➕ Registrar Nova Venda/Exame"):
    with st.form("form_otica"):
        cliente = st.text_input("Nome do Cliente")
        
        col1, col2 = st.columns(2)
        with col1:
            st.subheader("Olho Direito (OD)")
            od_esf = st.number_input("Esférico (OD)", step=0.25)
            od_cil = st.number_input("Cilíndrico (OD)", step=0.25)
            od_eixo = st.number_input("Eixo (OD)", min_value=0, max_value=180)
            
        with col2:
            st.subheader("Olho Esquerdo (OE)")
            oe_esf = st.number_input("Esférico (OE)", step=0.25)
            oe_cil = st.number_input("Cilíndrico (OE)", step=0.25)
            oe_eixo = st.number_input("Eixo (OE)", min_value=0, max_value=180)
            
        valor = st.number_input("Valor da Venda (R$)", min_value=0.0)
        
        if st.form_submit_button("Salvar Registro"):
            novo_registro = pd.DataFrame([[
                cliente, pd.Timestamp.now().strftime("%d/%m/%Y"), 
                od_esf, od_cil, od_eixo, oe_esf, oe_cil, oe_eixo, valor
            ]], columns=st.session_state.vendas_otica.columns)
            
            st.session_state.vendas_otica = pd.concat([st.session_state.vendas_otica, novo_registro], ignore_index=True)
            st.success("Registro salvo com sucesso!")

# --- VISUALIZAÇÃO ---
st.subheader("📋 Histórico de Clientes")
st.dataframe(st.session_state.vendas_otica, use_container_width=True)

# --- RESUMO FINANCEIRO ---
total = st.session_state.vendas_otica['Valor'].sum()
st.metric("Faturamento Total", f"R$ {total:.2f}")
