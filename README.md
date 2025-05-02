import { useState } from "react";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { motion } from "framer-motion";
import { Heart } from "lucide-react";

const emojis = ["💖", "🌈", "🐣", "✨", "🥺", "🌸", "😻", "🍭", "🦄", "💬"];

export default function YGChatApp() {
  const [messages, setMessages] = useState([]);
  const [input, setInput] = useState("");

  const sendMessage = () => {
    if (!input.trim()) return;
    setMessages([...messages, { text: input, emoji: emojis[Math.floor(Math.random() * emojis.length)] }]);
    setInput("");
  };

  return (
    <div className="min-h-screen bg-pink-100 flex flex-col items-center p-4">
      <motion.h1
        initial={{ opacity: 0, y: -50 }}
        animate={{ opacity: 1, y: 0 }}
        className="text-4xl font-bold text-pink-600 flex items-center gap-2"
      >
        YG <Heart className="text-red-500 w-6 h-6" /> Chat
      </motion.h1>
      <div className="w-full max-w-md mt-6">
        <Card className="rounded-2xl shadow-xl p-4 bg-white h-[60vh] overflow-y-auto">
          <CardContent className="space-y-3">
            {messages.map((msg, index) => (
              <motion.div
                key={index}
                initial={{ scale: 0.8, opacity: 0 }}
                animate={{ scale: 1, opacity: 1 }}
                className="bg-pink-200 rounded-xl p-3 text-pink-900"
              >
                {msg.emoji} {msg.text}
              </motion.div>
            ))}
          </CardContent>
        </Card>
        <div className="mt-4 flex gap-2">
          <Input
            value={input}
            onChange={(e) => setInput(e.target.value)}
            className="rounded-xl px-4"
            placeholder="Type something cute... ✨"
          />
          <Button onClick={sendMessage} className="rounded-xl bg-pink-400 hover:bg-pink-500 text-white">
            Send 💌
          </Button>
        </div>
      </div>
    </div>
  );
}
