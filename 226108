import streamlit as st
import anthropic

# ================================================
# ⚠️  COLOCA A TUA CHAVE AQUI
API_KEY = "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"
# ================================================

st.set_page_config(
    page_title="She — Assistente de Estudos",
    page_icon="📚",
    layout="centered",
    initial_sidebar_state="collapsed"
)

st.markdown("""
<style>
@import url('https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,400;1,9..144,300;1,9..144,400&family=Inter:wght@300;400;500;600&display=swap');

/* ── Reset & base ── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

html, body { background: #111009 !important; }

.stApp {
    background: #111009 !important;
    font-family: 'Inter', sans-serif;
    color: #E8E0D0;
}

/* Hide Streamlit chrome */
#MainMenu, footer, header, .stDeployButton,
[data-testid="stToolbar"], [data-testid="stDecoration"],
[data-testid="stStatusWidget"] { display: none !important; }

.block-container {
    padding: 0 !important;
    max-width: 100% !important;
}

/* ── Layout wrapper ── */
.she-wrap {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    background: #111009;
}

/* ── Header ── */
.she-header {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 18px 32px;
    border-bottom: 1px solid rgba(255,255,255,0.06);
    background: rgba(17,16,9,0.95);
    backdrop-filter: blur(12px);
    position: sticky;
    top: 0;
    z-index: 100;
}

.she-mark {
    width: 36px; height: 36px;
    border-radius: 10px;
    background: linear-gradient(135deg, #C9622A, #E8845A);
    display: flex; align-items: center; justify-content: center;
    font-family: 'Fraunces', serif;
    font-style: italic;
    color: #fff;
    font-size: 18px;
    font-weight: 300;
    box-shadow: 0 0 0 1px rgba(201,98,42,0.4), 0 4px 14px rgba(201,98,42,0.25);
}

.she-brand { display: flex; flex-direction: column; line-height: 1; }
.she-name {
    font-family: 'Fraunces', serif;
    font-style: italic;
    font-size: 19px;
    font-weight: 300;
    color: #E8E0D0;
    letter-spacing: 0.3px;
}
.she-tagline {
    font-size: 9.5px;
    letter-spacing: 2.2px;
    text-transform: uppercase;
    color: #6B6355;
    margin-top: 2px;
}

.she-badge {
    margin-left: auto;
    display: flex;
    align-items: center;
    gap: 7px;
    background: rgba(255,255,255,0.04);
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 8px;
    padding: 6px 12px;
    font-size: 11.5px;
    color: #6B6355;
}
.she-badge-dot {
    width: 5px; height: 5px;
    border-radius: 50%;
    background: #7BA87E;
    box-shadow: 0 0 6px rgba(123,168,126,0.6);
}
.she-badge-sep { opacity: 0.3; }

/* ── Onboarding cards ── */
.she-stage {
    min-height: calc(100vh - 61px);
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 48px 24px;
}

.she-card {
    width: 100%;
    max-width: 460px;
    text-align: center;
}

.she-steps {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 6px;
    margin-bottom: 40px;
}
.she-step {
    width: 6px; height: 6px;
    border-radius: 50%;
    background: rgba(255,255,255,0.1);
    transition: all 0.3s;
}
.she-step.active {
    width: 22px;
    border-radius: 3px;
    background: #C9622A;
}
.she-step.done {
    background: #7BA87E;
}

.she-eyebrow {
    font-size: 10px;
    letter-spacing: 2.5px;
    text-transform: uppercase;
    color: #C9622A;
    font-weight: 500;
    margin-bottom: 14px;
}

.she-heading {
    font-family: 'Fraunces', serif;
    font-style: italic;
    font-weight: 300;
    font-size: 38px;
    line-height: 1.15;
    color: #E8E0D0;
    margin-bottom: 10px;
    letter-spacing: -0.5px;
}

.she-desc {
    font-size: 14px;
    color: #6B6355;
    line-height: 1.6;
    margin-bottom: 36px;
}

/* ── Input overrides ── */
div[data-testid="stTextInput"] {
    margin-bottom: 10px;
}
div[data-testid="stTextInput"] > label { display: none; }
div[data-testid="stTextInput"] input {
    background: rgba(255,255,255,0.04) !important;
    border: 1px solid rgba(255,255,255,0.1) !important;
    border-radius: 12px !important;
    color: #E8E0D0 !important;
    font-family: 'Inter', sans-serif !important;
    font-size: 15px !important;
    padding: 14px 18px !important;
    transition: border-color 0.2s, box-shadow 0.2s !important;
    caret-color: #C9622A !important;
}
div[data-testid="stTextInput"] input::placeholder {
    color: #4A4338 !important;
}
div[data-testid="stTextInput"] input:focus {
    border-color: rgba(201,98,42,0.5) !important;
    box-shadow: 0 0 0 3px rgba(201,98,42,0.12) !important;
    outline: none !important;
}

/* ── Button overrides ── */
div[data-testid="stButton"] > button {
    width: 100% !important;
    background: #C9622A !important;
    color: #fff !important;
    border: none !important;
    border-radius: 12px !important;
    font-family: 'Inter', sans-serif !important;
    font-size: 14px !important;
    font-weight: 500 !important;
    padding: 13px 20px !important;
    letter-spacing: 0.2px !important;
    transition: all 0.2s !important;
    cursor: pointer !important;
}
div[data-testid="stButton"] > button:hover {
    background: #D97040 !important;
    transform: translateY(-1px) !important;
    box-shadow: 0 6px 20px rgba(201,98,42,0.3) !important;
}
div[data-testid="stButton"] > button:active {
    transform: translateY(0) !important;
}

/* ── Level cards (radio) ── */
div[data-testid="stRadio"] > label { display: none !important; }
div[data-testid="stRadio"] > div {
    display: grid !important;
    grid-template-columns: 1fr 1fr !important;
    gap: 10px !important;
    margin-bottom: 20px !important;
}
div[data-testid="stRadio"] > div > label {
    background: rgba(255,255,255,0.03) !important;
    border: 1px solid rgba(255,255,255,0.08) !important;
    border-radius: 14px !important;
    padding: 16px !important;
    cursor: pointer !important;
    transition: all 0.2s !important;
    display: flex !important;
    align-items: flex-start !important;
    gap: 10px !important;
}
div[data-testid="stRadio"] > div > label:hover {
    background: rgba(201,98,42,0.08) !important;
    border-color: rgba(201,98,42,0.3) !important;
}
div[data-testid="stRadio"] > div > label > div:first-child {
    margin-top: 2px !important;
    accent-color: #C9622A !important;
}
div[data-testid="stRadio"] [data-testid="stMarkdownContainer"] p {
    color: #E8E0D0 !important;
    font-size: 13.5px !important;
    font-weight: 500 !important;
    margin: 0 !important;
}

/* ── Chat shell ── */
.chat-body {
    max-width: 720px;
    margin: 0 auto;
    padding: 32px 24px 140px;
    width: 100%;
}

/* ── Messages ── */
.msg-row { display: flex; gap: 10px; margin-bottom: 16px; align-items: flex-end; }
.msg-row.user { flex-direction: row-reverse; }

.msg-avatar {
    width: 28px; height: 28px; border-radius: 9px;
    background: linear-gradient(135deg, #C9622A, #E8845A);
    display: flex; align-items: center; justify-content: center;
    font-family: 'Fraunces', serif; font-style: italic;
    color: #fff; font-size: 13px; font-weight: 300;
    flex-shrink: 0;
    box-shadow: 0 2px 8px rgba(201,98,42,0.3);
}

.msg-bubble {
    max-width: 72%;
    padding: 12px 16px;
    font-size: 14.5px;
    line-height: 1.6;
    white-space: pre-wrap;
    word-break: break-word;
}
.msg-bubble.she {
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(255,255,255,0.07);
    border-radius: 16px 16px 16px 4px;
    color: #E8E0D0;
}
.msg-bubble.user {
    background: #C9622A;
    border-radius: 16px 16px 4px 16px;
    color: #fff;
}
.msg-bubble.faded { opacity: 0.5; }

/* ── Depth picker ── */
.depth-card {
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(255,255,255,0.07);
    border-radius: 16px 16px 16px 4px;
    padding: 14px 16px;
    margin-left: 38px;
    margin-bottom: 16px;
}
.depth-label {
    font-size: 13px;
    color: #6B6355;
    margin-bottom: 12px;
}
.depth-cols { display: flex; gap: 8px; }
.depth-opt {
    flex: 1;
    background: rgba(255,255,255,0.04);
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 10px;
    padding: 10px 14px;
    font-size: 13px;
    font-weight: 500;
    color: #B0A898;
    cursor: pointer;
    text-align: center;
    transition: all 0.2s;
}
.depth-opt:hover { border-color: #C9622A; color: #E8E0D0; }

/* ── Typing indicator ── */
.typing-row { display: flex; gap: 10px; align-items: center; margin-bottom: 16px; }
.typing-bubble {
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(255,255,255,0.07);
    border-radius: 16px 16px 16px 4px;
    padding: 14px 18px;
    display: flex; gap: 5px; align-items: center;
}
.typing-dot {
    width: 6px; height: 6px;
    border-radius: 50%;
    background: #C9622A;
    animation: tdot 1.3s infinite ease-in-out;
}
.typing-dot:nth-child(2) { animation-delay: 0.15s; }
.typing-dot:nth-child(3) { animation-delay: 0.3s; }
@keyframes tdot {
    0%, 60%, 100% { transform: translateY(0); opacity: 0.4; }
    30% { transform: translateY(-4px); opacity: 1; }
}

/* ── Fixed input bar ── */
.chat-bar-wrap {
    position: fixed;
    bottom: 0; left: 0; right: 0;
    background: linear-gradient(to top, #111009 70%, transparent);
    padding: 20px 24px 24px;
    z-index: 50;
}
.chat-bar {
    max-width: 720px;
    margin: 0 auto;
    display: flex;
    gap: 10px;
    align-items: center;
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 14px;
    padding: 6px 6px 6px 16px;
    box-shadow: 0 8px 32px rgba(0,0,0,0.5);
    backdrop-filter: blur(12px);
}
.chat-bar input {
    flex: 1;
    background: transparent !important;
    border: none !important;
    color: #E8E0D0 !important;
    font-size: 14.5px !important;
    outline: none !important;
    font-family: 'Inter', sans-serif !important;
    padding: 8px 0 !important;
}
.chat-bar input::placeholder { color: #4A4338 !important; }
.send-btn {
    width: 36px; height: 36px;
    border-radius: 9px;
    background: #C9622A;
    border: none;
    cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    flex-shrink: 0;
    transition: all 0.2s;
    color: #fff;
}
.send-btn:hover { background: #D97040; transform: scale(1.05); }
.send-btn:disabled { opacity: 0.35; cursor: not-allowed; transform: none; }

/* ── Divider ── */
.she-divider {
    height: 1px;
    background: linear-gradient(to right, transparent, rgba(255,255,255,0.06), transparent);
    margin: 4px 0 24px;
}

/* ── Scrollbar ── */
::-webkit-scrollbar { width: 4px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.08); border-radius: 4px; }
</style>
""", unsafe_allow_html=True)

# ── Estado da sessão ──
for k, v in [("stage","name"),("name",""),("course",""),("level",""),
             ("messages",[]),("pending",None)]:
    if k not in st.session_state:
        st.session_state[k] = v

# ── Função de envio ──
def send_message(text, depth):
    di = ("O utilizador pediu uma resposta APROFUNDADA: explica com detalhes, contexto, exemplos e raciocínio completo."
          if depth == "deep"
          else "O utilizador pediu uma resposta RÁPIDA: sê direto, conciso, focando no essencial.")
    system = f"""És She, uma assistente de estudos inteligente e empática.
O nome do utilizador é {st.session_state.name}.
Está a cursar "{st.session_state.course}" no nível "{st.session_state.level}".
Usa o nome dele quando for natural. Adapta sempre a linguagem e profundidade ao curso e nível.
{di}
Sê didática, encorajadora e clara. Responde em português."""

    st.session_state.messages.append({"role": "user", "content": text})
    try:
        client = anthropic.Anthropic(api_key=API_KEY)
        resp = client.messages.create(
            model="claude-sonnet-4-6",
            max_tokens=1200,
            system=system,
            messages=st.session_state.messages,
        )
        reply = resp.content[0].text
    except Exception as e:
        reply = f"Ocorreu um erro: {e}"
    st.session_state.messages.append({"role": "assistant", "content": reply})
    st.session_state.pending = None

# ════════════════════════════════════════
# HEADER
# ════════════════════════════════════════
if st.session_state.stage == "chat":
    badge = f"""
    <div class="she-badge">
        <div class="she-badge-dot"></div>
        {st.session_state.name}
        <span class="she-badge-sep">·</span>
        {st.session_state.course}
        <span class="she-badge-sep">·</span>
        {st.session_state.level}
    </div>"""
else:
    badge = ""

st.markdown(f"""
<div class="she-header">
    <div class="she-mark">s</div>
    <div class="she-brand">
        <span class="she-name">she</span>
        <span class="she-tagline">assistente de estudos</span>
    </div>
    {badge}
</div>
""", unsafe_allow_html=True)

# ════════════════════════════════════════
# ETAPA 1 — NOME
# ════════════════════════════════════════
if st.session_state.stage == "name":
    st.markdown('<div class="she-stage"><div class="she-card">', unsafe_allow_html=True)
    st.markdown("""
    <div class="she-steps">
        <div class="she-step active"></div>
        <div class="she-step"></div>
        <div class="she-step"></div>
    </div>
    <p class="she-eyebrow">Bem-vindo</p>
    <h1 class="she-heading">Como devo chamar<br>você?</h1>
    <p class="she-desc">Assim posso falar contigo de um jeito mais próximo e pessoal.</p>
    """, unsafe_allow_html=True)

    name_val = st.text_input("nome", placeholder="O teu nome...", key="name_input", label_visibility="collapsed")
    if st.button("Continuar", key="btn_name"):
        if name_val.strip():
            st.session_state.name = name_val.strip()
            st.session_state.stage = "course"
            st.rerun()
        else:
            st.warning("Escreve o teu nome para continuar.")
    st.markdown('</div></div>', unsafe_allow_html=True)

# ════════════════════════════════════════
# ETAPA 2 — CURSO
# ════════════════════════════════════════
elif st.session_state.stage == "course":
    st.markdown('<div class="she-stage"><div class="she-card">', unsafe_allow_html=True)
    st.markdown(f"""
    <div class="she-steps">
        <div class="she-step done"></div>
        <div class="she-step active"></div>
        <div class="she-step"></div>
    </div>
    <p class="she-eyebrow">Olá, {st.session_state.name}</p>
    <h1 class="she-heading">Qual curso<br>estás a fazer?</h1>
    <p class="she-desc">Adapto cada resposta à tua área de estudo — com exemplos e linguagem do teu contexto.</p>
    """, unsafe_allow_html=True)

    course_val = st.text_input("curso", placeholder="Ex: Medicina, Direito, Engenharia...", key="course_input", label_visibility="collapsed")
    if st.button("Continuar", key="btn_course"):
        if course_val.strip():
            st.session_state.course = course_val.strip()
            st.session_state.stage = "level"
            st.rerun()
        else:
            st.warning("Escreve o teu curso para continuar.")
    st.markdown('</div></div>', unsafe_allow_html=True)

# ════════════════════════════════════════
# ETAPA 3 — NÍVEL
# ════════════════════════════════════════
elif st.session_state.stage == "level":
    st.markdown('<div class="she-stage"><div class="she-card">', unsafe_allow_html=True)
    st.markdown(f"""
    <div class="she-steps">
        <div class="she-step done"></div>
        <div class="she-step done"></div>
        <div class="she-step active"></div>
    </div>
    <p class="she-eyebrow">{st.session_state.course}</p>
    <h1 class="she-heading">Qual o teu nível<br>académico?</h1>
    <p class="she-desc">Isso ajusta a profundidade e a linguagem das respostas.</p>
    """, unsafe_allow_html=True)

    level_val = st.radio("nivel", [
        "Ensino Fundamental\n6º ao 9º ano",
        "Ensino Médio\n1ª à 3ª série",
        "Graduação\nuniversidade",
        "Pós-graduação\nespecialização, mestrado..."
    ], key="level_radio", label_visibility="collapsed")

    if st.button("Começar com a She →", key="btn_level"):
        st.session_state.level = level_val.split("\n")[0]
        st.session_state.stage = "chat"
        st.session_state.messages = [{
            "role": "assistant",
            "content": f"Olá, {st.session_state.name}! 👋\n\nEstou aqui para te ajudar com {st.session_state.course} ({st.session_state.level}). Podes perguntar o que quiseres — após cada pergunta escolhes se queres uma resposta rápida ou aprofundada, consoante o que precisas naquele momento."
        }]
        st.rerun()
    st.markdown('</div></div>', unsafe_allow_html=True)

# ════════════════════════════════════════
# CHAT
# ════════════════════════════════════════
elif st.session_state.stage == "chat":
    st.markdown('<div class="chat-body">', unsafe_allow_html=True)
    st.markdown('<div class="she-divider"></div>', unsafe_allow_html=True)

    # Histórico
    for msg in st.session_state.messages:
        if msg["role"] == "assistant":
            st.markdown(f"""
            <div class="msg-row">
                <div class="msg-avatar">s</div>
                <div class="msg-bubble she">{msg["content"]}</div>
            </div>""", unsafe_allow_html=True)
        else:
            st.markdown(f"""
            <div class="msg-row user">
                <div class="msg-bubble user">{msg["content"]}</div>
            </div>""", unsafe_allow_html=True)

    # Pergunta pendente
    if st.session_state.pending:
        st.markdown(f"""
        <div class="msg-row user">
            <div class="msg-bubble user faded">{st.session_state.pending}</div>
        </div>
        <div class="depth-card">
            <div class="depth-label">Quer uma resposta rápida ou aprofundada?</div>
        </div>""", unsafe_allow_html=True)

        col1, col2 = st.columns(2)
        with col1:
            if st.button("⚡  Rápida", key="btn_quick"):
                send_message(st.session_state.pending, "quick")
                st.rerun()
        with col2:
            if st.button("🔎  Aprofundada", key="btn_deep"):
                send_message(st.session_state.pending, "deep")
                st.rerun()
    else:
        # Input
        st.markdown('<div style="height:80px"></div>', unsafe_allow_html=True)
        user_input = st.text_input("msg", placeholder="Pergunta alguma coisa sobre os teus estudos...",
                                    key="chat_input", label_visibility="collapsed")
        if st.button("Enviar →", key="btn_send"):
            if user_input.strip():
                st.session_state.pending = user_input.strip()
                st.rerun()

    st.markdown('</div>', unsafe_allow_html=True)
