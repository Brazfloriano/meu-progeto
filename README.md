import React, { useState } from "react";

const materias = [
  "Matemática", "Português", "História", "Geografia",
  "Ciências", "Inglês", "Física", "Química", "Biologia"
];

const horariosPadrao = [
  { hora: "08:00", materia: "Matemática" },
  { hora: "09:00", materia: "Português" },
  { hora: "10:00", materia: "História" },
  { hora: "11:00", materia: "Geografia" },
  { hora: "13:00", materia: "Ciências" },
  { hora: "14:00", materia: "Inglês" }
];

const videoAulas = [
  {
    titulo: "Soma e Subtração",
    materia: "Matemática",
    url: "https://www.youtube.com/embed/KfF5MXiHqVU"
  },
  {
    titulo: "Verbos no presente",
    materia: "Português",
    url: "https://www.youtube.com/embed/6N5nZclOuaE"
  },
  {
    titulo: "Revolução Francesa",
    materia: "História",
    url: "https://www.youtube.com/embed/B3yKQcqGfF4"
  }
];

const frasesBiblia = [
  "Tudo posso naquele que me fortalece. (Filipenses 4:13)",
  "Confia no Senhor de todo o teu coração. (Provérbios 3:5)",
  "O Senhor é o meu pastor e nada me faltará. (Salmo 23:1)"
];

export default function EstudaFacilApp() {
  const [loggedIn, setLoggedIn] = useState(false);
  const [name, setName] = useState("");
  const [search, setSearch] = useState("");
  const [frase, setFrase] = useState(
    frasesBiblia[Math.floor(Math.random() * frasesBiblia.length)]
  );

  const handleLogin = () => {
    if (name.trim()) setLoggedIn(true);
  };

  const filteredMaterias = materias.filter((m) =>
    m.toLowerCase().includes(search.toLowerCase())
  );

  return (
    <div style={{ 
      minHeight: "100vh", 
      background: "linear-gradient(to bottom right, #bfdbfe, #c7d2fe)", 
      display: "flex", 
      justifyContent: "center", 
      padding: "20px", 
      fontFamily: "Arial, sans-serif" 
    }}>
      <div style={{ maxWidth: 400, width: "100%", background: "white", borderRadius: 20, padding: 20, boxShadow: "0 10px 15px rgba(0,0,0,0.1)" }}>
        <h1 style={{ color: "#1e40af", fontWeight: "bold", marginBottom: 20 }}>📘 EstudaFácil</h1>

        {!loggedIn ? (
          <>
            <h2 style={{ marginBottom: 15 }}>Bem-vindo ao EstudaFácil!</h2>
            <input
              type="text"
              placeholder="Seu nome..."
              value={name}
              onChange={(e) => setName(e.target.value)}
              style={{ width: "100%", padding: 10, borderRadius: 10, border: "1px solid #ddd", marginBottom: 20 }}
            />
            <button
              onClick={handleLogin}
              style={{ width: "100%", padding: 10, backgroundColor: "#2563eb", color: "white", border: "none", borderRadius: 10, cursor: "pointer" }}
            >
              Começar a Estudar
            </button>
          </>
        ) : (
          <>
            <div style={{ marginBottom: 20 }}>
              <h2>Olá, {name}! 👋</h2>
              <p style={{ fontStyle: "italic", color: "#6b21a8" }}>📖 {frase}</p>
            </div>

            <div style={{ marginBottom: 20 }}>
              <h3>📚 Pastas de Matérias</h3>
              <input
                type="text"
                placeholder="Buscar matéria..."
                value={search}
                onChange={(e) => setSearch(e.target.value)}
                style={{ width: "100%", padding: 8, borderRadius: 10, border: "1px solid #ddd", marginBottom: 10 }}
              />
              <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 10 }}>
                {filteredMaterias.map((materia, i) => (
                  <div key={i} style={{ background: "#f3f4f6", padding: 10, borderRadius: 12, textAlign: "center", fontWeight: "600" }}>
                    {materia}
                  </div>
                ))}
              </div>
            </div>

            <div style={{ marginBottom: 20 }}>
              <h3>🕒 Estudo Diário</h3>
              <ul style={{ listStyle: "none", paddingLeft: 0 }}>
                {horariosPadrao.map((item, i) => (
                  <li key={i} style={{ background: "#f3f4f6", padding: 10, borderRadius: 12, marginBottom: 6, display: "flex", justifyContent: "space-between" }}>
                    <span style={{ fontWeight: "600" }}>{item.hora}</span>
                    <span>{item.materia}</span>
                  </li>
                ))}
              </ul>
            </div>

            <div style={{ marginBottom: 20 }}>
              <h3>🎥 Videoaulas</h3>
              {videoAulas.map((video, i) => (
                <div key={i} style={{ marginBottom: 15 }}>
                  <div style={{ fontWeight: "600", marginBottom: 6 }}>
                    ▶️ {video.materia} — {video.titulo}
                  </div>
                  <div style={{ position: "relative", paddingBottom: "56.25%", height: 0, overflow: "hidden", borderRadius: 15 }}>
                    <iframe
                      src={video.url}
                      title={video.titulo}
                      frameBorder="0"
                      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                      allowFullScreen
                      style={{ position: "absolute", top: 0, left: 0, width: "100%", height: "100%", borderRadius: 15 }}
                    />
                  </div>
                </div>
              ))}
            </div>

            <div style={{ textAlign: "center" }}>
              <h3>💳 Apoie o projeto</h3>
              <p style={{ marginBottom: 10, color: "#4b5563" }}>
                Ajude a manter a plataforma ativa e receba recursos extras!
              </p>
              <a
                href="https://buy.stripe.com/test_abc123"
                target="_blank"
                rel="noopener noreferrer"
                style={{
                  display: "inline-block",
                  padding: "10px 20px",
                  backgroundColor: "#2563eb",
                  color: "white",
                  borderRadius: 12,
                  textDecoration: "none",
                  fontWeight: "600",
                  cursor: "pointer"
                }}
              >
                💳 Apoiar com Stripe
              </a>
            </div>
          </>
        )}
      </div>
    </div>
  );
}
