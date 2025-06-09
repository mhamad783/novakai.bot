
import React, { useState, useEffect, useRef } from 'react'; import './index.css';

const NovaKaiLanding = () => { const [scrolled, setScrolled] = useState(false); const statsRef = useRef(null);

const inviteURL = 'https://discord.com/oauth2/authorize?client_id=1372146394701496392&scope=bot&permissions=8';

const features = [ { icon: '🛡️', title: 'Advanced Moderation', description: 'Auto-mod, ban/kick, warnings, and filtering.' }, { icon: '🎮', title: 'Fun & Games', description: 'Mini-games, memes, and more.' }, { icon: '⚡', title: 'Fast & Reliable', description: '99.9% uptime and instant responses.' }, { icon: '⚙️', title: 'Easy Setup', description: 'Quick commands to get started.' }, { icon: '🔒', title: 'Secure & Safe', description: 'Security-focused and trusted.' }, { icon: '🎯', title: 'Smart Detection', description: 'Spam filtering and auto actions.' } ];

const commands = [ { command: '!ban @user', description: 'Ban a user from the server.' }, { command: '!kick @user', description: 'Kick a user from the server.' }, { command: '!warn @user', description: 'Warn a user for breaking rules.' }, { command: '!mute @user', description: 'Temporarily mute a user.' }, { command: '!clear [number]', description: 'Delete messages quickly.' }, { command: '!meme', description: 'Send a random meme.' }, { command: '!8ball [question]', description: 'Ask the 8ball.' }, { command: '!joke', description: 'Send a random joke.' } ];

const stats = [ { number: '10K+', label: 'Servers' }, { number: '500K+', label: 'Users' }, { number: '99.9%', label: 'Uptime' }, { number: '24/7', label: 'Support' } ];

useEffect(() => { const onScroll = () => setScrolled(window.scrollY > 100); window.addEventListener('scroll', onScroll); return () => window.removeEventListener('scroll', onScroll); }, []);

const scrollTo = (id) => { const el = document.getElementById(id); if (el) el.scrollIntoView({ behavior: 'smooth' }); };

return ( <div className="font-sans"> <style>{@keyframes float { 0% { transform: translate(0, 0) rotate(0deg); } 100% { transform: translate(-50px, -50px) rotate(360deg); } } .float-animation { animation: float 20s infinite linear; }}</style>

<header className={`fixed top-0 w-full z-50 transition-all ${scrolled ? 'bg-indigo-600/90 backdrop-blur' : 'bg-indigo-600'}`}>
    <nav className="flex justify-between items-center px-6 py-4 text-white max-w-6xl mx-auto">
      <div className="text-xl font-bold">🤖 NovaKai</div>
      <div className="hidden md:flex gap-6">
        <button onClick={() => scrollTo('features')} className="hover:opacity-80">Features</button>
        <button onClick={() => scrollTo('commands')} className="hover:opacity-80">Commands</button>
        <button onClick={() => scrollTo('support')} className="hover:opacity-80">Support</button>
        <button onClick={() => window.open(inviteURL)} className="hover:opacity-80">Invite</button>
      </div>
    </nav>
  </header>

  <section className="hero-background bg-gradient-to-r from-indigo-600 to-blue-500 text-white pt-32 pb-16 text-center px-4 relative">
    <div className="float-animation absolute inset-0 opacity-10" />
    <div className="relative z-10">
      <h1 className="text-5xl md:text-6xl font-bold mb-6">NovaKai</h1>
      <p className="text-xl max-w-2xl mx-auto mb-8">Your all-in-one moderation and fun Discord bot.</p>
      <div className="flex flex-col sm:flex-row gap-4 justify-center">
        <button onClick={() => window.open(inviteURL)} className="bg-emerald-500 px-6 py-3 rounded-lg hover:bg-emerald-600">Add to Discord</button>
        <button onClick={() => scrollTo('features')} className="bg-white/20 border border-white/30 px-6 py-3 rounded-lg hover:bg-white/30">Learn More</button>
      </div>
    </div>
  </section>

  <section ref={statsRef} className="bg-gray-800 text-white py-16 text-center">
    <div className="grid grid-cols-2 md:grid-cols-4 gap-8 max-w-4xl mx-auto">
      {stats.map((s, i) => (
        <div key={i} className="hover:scale-105 transition-transform">
          <h3 className="text-4xl font-bold text-emerald-400">{s.number}</h3>
          <p>{s.label}</p>
        </div>
      ))}
    </div>
  </section>

  <section id="features" className="py-16 bg-gray-50 text-center">
    <h2 className="text-4xl font-bold mb-12">Amazing Features</h2>
    <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 max-w-6xl mx-auto px-4">
      {features.map((f, i) => (
        <div key={i} className="bg-white rounded-xl p-6 shadow hover:shadow-lg">
          <div className="text-3xl mb-4">{f.icon}</div>
          <h3 className="font-semibold text-xl mb-2">{f.title}</h3>
          <p className="text-gray-600">{f.description}</p>
        </div>
      ))}
    </div>
  </section>

  <section id="commands" className="py-16 bg-white">
    <h2 className="text-4xl font-bold text-center mb-12">Popular Commands</h2>
    <div className="grid grid-cols-1 md:grid-cols-2 gap-6 max-w-6xl mx-auto px-4">
      {commands.map((cmd, i) => (
        <div key={i} className="bg-gray-100 p-4 border-l-4 border-indigo-600 rounded">
          <h4 className="font-mono font-bold text-indigo-600">{cmd.command}</h4>
          <p>{cmd.description}</p>
        </div>
      ))}
    </div>
  </section>

  <footer id="support" className="bg-gray-800 text-white py-8 text-center">
    <p className="text-sm text-gray-400">&copy; 2025 NovaKai — All rights reserved.</p>
  </footer>
</div>

); };

export default NovaKaiLanding;

