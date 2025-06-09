import React, { useState, useEffect, useRef } from 'react'; import './index.css';

const NovaKaiLanding = () => { const [scrolled, setScrolled] = useState(false); const statsRef = useRef(null);

const inviteURL = 'https://discord.com/oauth2/authorize?client_id=1372146394701496392&scope=bot&permissions=8';

const features = [ { icon: '🛡️', title: 'Advanced Moderation', description: 'Auto-mod, ban/kick, warnings, and filtering.' }, { icon: '🎮', title: 'Fun & Games', description: 'Mini-games, memes, and more.' }, { icon: '⚡', title: 'Fast & Reliable', description: '99.9% uptime and instant responses.' }, { icon: '⚙️', title: 'Easy Setup', description: 'Quick commands to get started.' }, { icon: '🔒', title: 'Secure & Safe', description: 'Security-focused and trusted.' }, { icon: '🎯', title: 'Smart Detection', description: 'Spam filtering and auto actions.' } ];

const commands = [ { command: '!ban @user', description: 'Ban a user from the server.' }, { command: '!kick @user', description: 'Kick a user from the server.' }, { command: '!warn @user', description: 'Warn a user for breaking rules.' }, { command: '!mute @user', description: 'Temporarily mute a user.' }, { command: '!clear [number]', description: 'Delete messages quickly.' }, { command: '!meme', description: 'Send a random meme.' }, { command: '!8ball [question]', description: 'Ask the 8ball.' }, { command: '!joke', description: 'Send a random joke.' } ];

const stats = [ { number: '10K+', label: 'Servers' }, { number: '500K+', label: 'Users' }, { number: '99.9%', label: 'Uptime' }, { number: '24/7', label: 'Support' } ];

useEffect(() => { const onScroll = () => setScrolled(window.scrollY >


