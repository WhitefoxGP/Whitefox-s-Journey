# Whitefox-s-Journey
Jurnal moto
'use client'

import { useState } from "react";

export default function Home() {
  const [posts, setPosts] = useState([
    {
      title: "Prima mea tură lungă",
      date: "Mai 2025",
      content:
        "Prima experiență pe distanță lungă – emoții, adrenalină și libertatea drumului deschis. A fost momentul în care am simțit că motociclismul devine parte din mine.",
    },
    {
      title: "Drumul Transfăgărășan",
      date: "Iunie 2025",
      content:
        "Serpentine spectaculoase, peisaje incredibile și una dintre cele mai frumoase experiențe pe două roți. O experiență pe care o recomand oricărei motocicliste pasionate de aventură.",
    },
  ]);

  const [showForm, setShowForm] = useState(false);
  const [newPost, setNewPost] = useState({ title: "", content: "" });

  const addPost = () => {
    if (!newPost.title || !newPost.content) return;

    const today = new Date();
    const formattedDate = today.toLocaleDateString("ro-RO", {
      year: "numeric",
      month: "long",
    });

    setPosts([
      {
        title: newPost.title,
        content: newPost.content,
        date: formattedDate,
      },
      ...posts,
    ]);

    setNewPost({ title: "", content: "" });
    setShowForm(false);
  };

  return (
    <main className="min-h-screen bg-gray-100 p-6">
      <div className="max-w-4xl mx-auto">
        {/* Header */}
        <div className="text-center mb-10">
          <h1 className="text-4xl font-bold mb-2">
            Jurnalul meu pe două roți 🏍️
          </h1>
          <p className="text-gray-600 text-lg">
            Aventuri, trasee și lecții învățate din experiențele mele de motociclistă.
          </p>
        </div>

        {/* Add Post Button */}
        <div className="flex justify-end mb-6">
          <button
            onClick={() => setShowForm(!showForm)}
            className="bg-black text-white px-4 py-2 rounded-xl hover:opacity-80 transition"
          >
            Adaugă experiență
          </button>
        </div>

        {/* Form */}
        {showForm && (
          <div className="bg-white p-6 rounded-2xl shadow-md mb-8">
            <input
              type="text"
              placeholder="Titlu experiență"
              value={newPost.title}
              onChange={(e) =>
                setNewPost({ ...newPost, title: e.target.value })
              }
              className="w-full mb-4 p-3 border rounded-lg"
            />
            <textarea
              placeholder="Scrie experiența ta aici..."
              value={newPost.content}
              onChange={(e) =>
                setNewPost({ ...newPost, content: e.target.value })
              }
              className="w-full mb-4 p-3 border rounded-lg h-32"
            />
            <button
              onClick={addPost}
              className="bg-black text-white px-4 py-2 rounded-xl hover:opacity-80 transition"
            >
              Publică
            </button>
          </div>
        )}

        {/* Posts */}
        <div className="space-y-6">
          {posts.map((post, index) => (
            <div
              key={index}
              className="bg-white p-6 rounded-2xl shadow-md"
            >
              <h2 className="text-2xl font-semibold mb-2">
                {post.title}
              </h2>
              <p className="text-sm text-gray-500 mb-3">
                {post.date}
              </p>
              <p className="text-gray-700 whitespace-pre-line">
                {post.content}
              </p>
            </div>
          ))}
        </div>

        {/* Footer */}
        <div className="text-center mt-16 text-gray-500 text-sm">
          © {new Date().getFullYear()} Jurnal Moto · Creat cu pasiune pentru drumuri
        </div>
      </div>
    </main>
  );
}
