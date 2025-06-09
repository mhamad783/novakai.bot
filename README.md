import React, { useState, useEffect, useRef } from 'react';

const NovaKaiLanding = () => {
  const [scrolled, setScrolled] = useState(false);
  const [countersAnimated, setCountersAnimated] = useState(false);
  const statsRef = useRef(null);

  const inviteURL = 'https://discord.com/oauth2/authorize?client_id=1372146394701496392&scope=bot&permissions=8';

  const features = [
    {
      icon: '🛡️',
      title: 'Advanced Moderation',
      description: 'Powerful moderation tools including auto-mod, ban/kick commands, warning system, and message filtering to keep your server safe.'
    },
    {
      icon: '🎮',
      title: 'Fun & Games',
      description: 'Entertaining commands, mini-games, memes, and interactive features to keep your community engaged and active.'
    },
    {
      icon: '⚡',
      title: 'Fast & Reliable',
      description: 'Lightning-fast response times with 99.9% uptime. NovaKai is always ready to help moderate your server.'
    },
    {
      icon: '⚙️',
      title: 'Easy Setup',
      description: 'Simple commands and intuitive setup process. Get NovaKai working in your server within minutes.'
    },
    {
      icon: '🔒',
      title: 'Secure & Safe',
      description: 'Built with security in mind. Your server data is protected with industry-standard security measures.'
    },
    {
      icon: '🎯',
      title: 'Smart Detection',
      description: 'Intelligent spam detection, inappropriate content filtering, and automated moderation actions.'
    }
  ];

  const commands = [
    { command: '!ban @user [reason]', description: 'Ban a user from the server with optional reason' },
    { command: '!kick @user [reason]', description: 'Kick a user from the server temporarily' },
    { command: '!warn @user [reason]', description: 'Give a warning to a user for breaking rules' },
    { command: '!mute @user [time]', description: 'Temporarily mute a user in the server' },
    { command: '!clear [number]', description: 'Delete multiple messages at once' },
    { command: '!meme', description: 'Get random funny memes to share' },
    { command: '!8ball [question]', description: 'Ask the magic 8-ball a question' },
    { command: '!joke', description: 'Get a random joke to lighten the mood' }
  ];

  const stats = [
    { number: '10K+', label: 'Servers' },
    { number: '500K+', label: 'Users' },
    { number: '99.9%', label: 'Uptime' },
    { number: '24/7', label: 'Support' }
  ];

  useEffect(() => {
    const handleScroll = () => {
      setScrolled(window.scrollY > 100);
    };

    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  useEffect(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting && !countersAnimated) {
            setCountersAnimated(true);
          }
        });
      },
      { threshold: 0.5 }
    );

    if (statsRef.current) {
      observer.observe(statsRef.current);
    }

    return () => observer.disconnect();
  }, [countersAnimated]);

  const scrollToSection = (sectionId) => {
    const element = document.getElementById(sectionId);
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' });
    }
  };

  const handleInviteClick = () => {
    window.open(inviteURL, '_blank');
  };

  return (
    <div className="min-h-screen bg-white overflow-x-hidden">
      <style jsx>{`
        @keyframes float {
          0% { transform: translate(0, 0) rotate(0deg); }
          100% { transform: translate(-50px, -50px) rotate(360deg); }
        }
        .float-animation {
          animation: float 20s infinite linear;
        }
        .hero-background::before {
          content: '';
          position: absolute;
          width: 200%;
          height: 200%;
          background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><circle cx="20" cy="20" r="2" fill="rgba(255,255,255,0.1)"/><circle cx="80" cy="40" r="1" fill="rgba(255,255,255,0.1)"/><circle cx="40" cy="80" r="1.5" fill="rgba(255,255,255,0.1)"/></svg>');
          top: -50%;
          left: -50%;
        }
        .gradient-text {
          background: linear-gradient(45deg, #fff, #e0e7ff);
          -webkit-background-clip: text;
          -webkit-text-fill-color: transparent;
          background-clip: text;
        }
      `}</style>

      {/* Header */}
      <header className={`fixed w-full top-0 z-50 transition-all duration-300 ${
        scrolled ? 'bg-indigo-600/95 backdrop-blur-md' : 'bg-gradient-to-r from-indigo-600 to-blue-500'
      }`}>
        <nav className="flex justify-between items-center max-w-6xl mx-auto px-8 py-4">
          <div className="flex items-center gap-2 text-white text-xl font-bold">
            <span>🤖</span>
            NovaKai
          </div>
          <ul className="hidden md:flex gap-8">
            {['features', 'commands', 'support'].map(item => (
              <li key={item}>
                <button 
                  onClick={() => scrollToSection(item)}
                  className="text-white hover:opacity-80 transition-opacity capitalize"
                >
                  {item}
                </button>
              </li>
            ))}
            <li>
              <button 
                onClick={handleInviteClick}
                className="text-white hover:opacity-80 transition-opacity"
              >
                Invite
              </button>
            </li>
          </ul>
        </nav>
      </header>

      {/* Hero Section */}
      <section className="hero-background relative bg-gradient-to-r from-indigo-600 to-blue-500 text-white pt-32 pb-16 px-8 text-center overflow-hidden">
        <div className="float-animation absolute inset-0 opacity-10"></div>
        <div className="relative z-10 max-w-4xl mx-auto">
          <h1 className="gradient-text text-6xl md:text-7xl font-bold mb-6">
            NovaKai
          </h1>
          <p className="text-xl md:text-2xl mb-8 opacity-90 max-w-3xl mx-auto">
            The ultimate Discord moderation and fun bot to keep your server safe, organized, and entertaining for everyone.
          </p>
          <div className="flex flex-col sm:flex-row gap-4 justify-center">
            <button
              onClick={handleInviteClick}
              className="bg-emerald-500 hover:bg-emerald-600 text-white px-8 py-4 rounded-lg text-lg font-semibold transition-all duration-300 transform hover:scale-105 hover:shadow-xl"
            >
              Add to Discord
            </button>
            <button
              onClick={() => scrollToSection('features')}
              className="bg-white/10 hover:bg-white/20 text-white border-2 border-white/30 px-8 py-4 rounded-lg text-lg font-semibold transition-all duration-300 transform hover:scale-105"
            >
              Learn More
            </button>
          </div>
        </div>
      </section>

      {/* Stats Section */}
      <section ref={statsRef} className="bg-gradient-to-r from-gray-800 to-gray-700 text-white py-16 px-8 text-center">
        <div className="max-w-4xl mx-auto">
          <div className="grid grid-cols-2 md:grid-cols-4 gap-8">
            {stats.map((stat, index) => (
              <div key={index} className="transform hover:scale-105 transition-transform">
                <h3 className="text-4xl md:text-5xl font-bold text-emerald-400 mb-2">
                  {stat.number}
                </h3>
                <p className="text-lg opacity-90">{stat.label}</p>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Features Section */}
      <section id="features" className="bg-gray-50 py-16 px-8">
        <div className="max-w-6xl mx-auto">
          <h2 className="text-4xl md:text-5xl font-bold text-center mb-12 text-gray-800">
            Amazing Features
          </h2>
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            {features.map((feature, index) => (
              <div
                key={index}
                className="bg-white rounded-xl p-8 text-center shadow-lg hover:shadow-xl transform hover:scale-105 transition-all duration-300"
              >
                <div className="w-16 h-16 bg-gradient-to-r from-indigo-600 to-blue-500 rounded-full flex items-center justify-center text-2xl mx-auto mb-6">
                  {feature.icon}
                </div>
                <h3 className="text-xl font-bold mb-4 text-gray-800">
                  {feature.title}
                </h3>
                <p className="text-gray-600 leading-relaxed">
                  {feature.description}
                </p>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Commands Section */}
      <section id="commands" className="bg-white py-16 px-8">
        <div className="max-w-6xl mx-auto">
          <h2 className="text-4xl md:text-5xl font-bold text-center mb-12 text-gray-800">
            Popular Commands
          </h2>
          <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
            {commands.map((cmd, index) => (
              <div
                key={index}
                className="bg-gray-50 rounded-lg p-6 border-l-4 border-indigo-600 hover:shadow-lg transition-shadow"
              >
                <h4 className="font-mono text-lg font-semibold mb-2 text-gray-800">
                  {cmd.command}
                </h4>
                <p className="text-gray-600">{cmd.description}</p>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer id="support" className="bg-gray-800 text-white py-8 px-8 text-center">
        <div className="max-w-6xl mx-auto">
          <div className="flex flex-wrap justify-center gap-8 mb-6">
            {['Privacy Policy', 'Terms of Service', 'Support Server', 'Documentation', 'Status'].map(link => (
              <a
                key={link}
                href="#"
                className="text-gray-400 hover:text-white transition-colors"
              >
                {link}
              </a>
            ))}
          </div>
          <p className="text-gray-400">
            &copy; 2025 NovaKai. Made with ❤️ for Discord communities.
          </p>
        </div>
      </footer>
    </div>
  );
};

export default NovaKaiLanding;