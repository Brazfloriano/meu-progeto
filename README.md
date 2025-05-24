// SaaS EstudaFácil – versão com cobrança via Stripe (sem videoaulas)
import { useState } from "react";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Card } from "@/components/ui/card";
import { motion } from "framer-motion";
import { Search, CreditCard } from "lucide-react";

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
    <div className="min-h-screen flex flex-col items-center bg-gradient-to-br from-blue-100 to-purple-200 p-4">
      <h1 className="text-2xl font-bold text-blue-800 mb-4">📘 EstudaFácil</h1>

      <motion.div initial={{ opacity: 0, y: -30 }} animate={{ opacity: 1, y: 0 }} className="w-full max-w-md">
        {!loggedIn ? (
          <Card className="rounded-2xl shadow-lg p-6">
            <h2 className="text-xl font-bold mb-4">Bem-vindo ao EstudaFácil!</h2>
            <Input
              placeholder="Seu nome..."
              value={name}
              onChange={(e) => setName(e.target.value)}
              className="mb-4"
            />
            <Button onClick={handleLogin} className="w-full">
              Começar a Estudar
            </Button>
          </Card>
        ) : (
          <Card className="rounded-2xl shadow-lg p-6 space-y-6">
            <div>
              <h2 className="text-xl font-semibold mb-2">Olá, {name}! 👋</h2>
              <p className="italic text-sm text-purple-700">📖 {frase}</p>
            </div>

            <div>
              <h3 className="text-lg font-medium mb-2">📚 Pastas de Matérias</h3>
              <div className="mb-4 flex items-center gap-2">
                <Search className="w-5 h-5 text-gray-500" />
                <Input placeholder="Buscar matéria..." value={search} onChange={(e) => setSearch(e.target.value)} />
              </div>
              <div className="grid grid-cols-2 gap-3">
                {filteredMaterias.map((materia, index) => (
                  <div key={index} className="bg-white rounded-xl p-3 shadow text-center text-sm font-medium">
                    {materia}
                  </div>
                ))}
              </div>
            </div>

            <div>
              <h3 className="text-lg font-medium mb-2">🕒 Estudo Diário</h3>
              <ul className="text-sm space-y-2">
                {horariosPadrao.map((item, index) => (
                  <li key={index} className="bg-white rounded-xl shadow p-3 flex justify-between items-center">
                    <span className="font-semibold">{item.hora}</span>
                    <span>{item.materia}</span>
                  </li>
                ))}
              </ul>
            </div>

            <div>
              <h3 className="text-lg font-medium mb-2">💳 Apoie o projeto</h3>
              <p className="text-sm text-gray-600 mb-3">Ajude a manter a plataforma ativa e receba recursos extras!</p>
              <a
                href="https://buy.stripe.com/test_abc123" // Substitua com seu link real do Stripe
                target="_blank"
                rel="noopener noreferrer"
                className="inline-flex items-center gap-2 bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded-xl shadow"
              >
                <CreditCard className="w-5 h-5" /> Apoiar com Stripe
              </a>
            </div>
          </Card>
        )}
      </motion.div>
    </div>
  );
}
