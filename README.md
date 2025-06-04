import React, { useState } from 'react';
import { 
  Home, 
  User, 
  Wallet, 
  Settings, 
  Plus, 
  Heart, 
  MessageCircle, 
  Share, 
  TrendingUp,
  Bell,
  Search,
  ChevronRight,
  Star,
  Coins,
  Lock,
  Users,
  Edit3,
  ExternalLink
} from 'lucide-react';

const PathLogo = () => (
  <div className="flex items-center space-x-2">
    <div className="w-8 h-8 bg-green-500 rounded-full flex items-center justify-center">
      <div className="w-6 h-6 relative">
        <div className="absolute inset-0 border-2 border-white rounded-full"></div>
        <div className="absolute top-1 left-1 w-1 h-1 bg-white rounded-full"></div>
        <div className="absolute bottom-1 right-1 w-1 h-1 bg-white rounded-full"></div>
        <div className="absolute top-1 right-1 bottom-1 left-1 border border-white transform rotate-45"></div>
      </div>
    </div>
    <span className="text-xl font-bold text-white">PATH</span>
  </div>
);

const WireframeApp = () => {
  const [currentPage, setCurrentPage] = useState('landing');
  const [isWalletConnected, setIsWalletConnected] = useState(false);

  const navigationPages = [
    { id: 'landing', name: 'Landing', icon: Home },
    { id: 'feed', name: 'Feed', icon: TrendingUp },
    { id: 'profile', name: 'Creator Profile', icon: User },
    { id: 'dashboard', name: 'Token Dashboard', icon: Wallet },
    { id: 'onboarding', name: 'Creator Onboarding', icon: Plus },
    { id: 'settings', name: 'Settings', icon: Settings },
  ];

  const NavBar = ({ isLanding = false }) => (
    <nav className={`${isLanding ? 'absolute top-0 left-0 right-0 z-50' : 'sticky top-0'} bg-black border-b border-gray-800 px-4 py-3`}>
      <div className="max-w-7xl mx-auto flex items-center justify-between">
        <PathLogo />
        
        {!isLanding && (
          <div className="hidden md:flex items-center space-x-6">
            <button className="text-gray-300 hover:text-white flex items-center space-x-1">
              <Search size={18} />
              <span>Search</span>
            </button>
            <button className="text-gray-300 hover:text-white">
              <Bell size={18} />
            </button>
          </div>
        )}
        
        <div className="flex items-center space-x-3">
          {isWalletConnected ? (
            <div className="flex items-center space-x-2 bg-green-500 px-3 py-1 rounded-full">
              <Wallet size={16} />
              <span className="text-black font-medium">Connected</span>
            </div>
          ) : (
            <button 
              onClick={() => setIsWalletConnected(true)}
              className="bg-green-500 hover:bg-green-600 text-black px-4 py-2 rounded-full font-medium"
            >
              Connect Wallet
            </button>
          )}
        </div>
      </div>
    </nav>
  );

  const Sidebar = ({ currentPage, setCurrentPage }) => (
    <div className="hidden md:block w-64 bg-gray-900 border-r border-gray-800 min-h-screen">
      <div className="p-4">
        <div className="space-y-2">
          {navigationPages.map((page) => {
            const Icon = page.icon;
            return (
              <button
                key={page.id}
                onClick={() => setCurrentPage(page.id)}
                className={`w-full flex items-center space-x-3 px-3 py-2 rounded-lg transition-colors ${
                  currentPage === page.id 
                    ? 'bg-green-500/20 text-green-500' 
                    : 'text-gray-300 hover:bg-gray-800 hover:text-white'
                }`}
              >
                <Icon size={20} />
                <span>{page.name}</span>
              </button>
            );
          })}
        </div>
      </div>
    </div>
  );

  const MobileNav = ({ currentPage, setCurrentPage }) => (
    <div className="md:hidden fixed bottom-0 left-0 right-0 bg-black border-t border-gray-800 px-4 py-2">
      <div className="flex justify-around">
        {navigationPages.slice(0, 5).map((page) => {
          const Icon = page.icon;
          return (
            <button
              key={page.id}
              onClick={() => setCurrentPage(page.id)}
              className={`flex flex-col items-center space-y-1 p-2 ${
                currentPage === page.id ? 'text-green-500' : 'text-gray-400'
              }`}
            >
              <Icon size={20} />
              <span className="text-xs">{page.name}</span>
            </button>
          );
        })}
      </div>
    </div>
  );

  const LandingPage = () => (
    <div className="min-h-screen bg-black text-white">
      <NavBar isLanding={true} />
      
      {/* Hero Section */}
      <div className="pt-20 pb-16 px-4">
        <div className="max-w-4xl mx-auto text-center">
          <h1 className="text-5xl md:text-7xl font-bold mb-6">
            The Future of
            <span className="text-green-500"> Creator Economy</span>
          </h1>
          <p className="text-xl md:text-2xl text-gray-300 mb-8 max-w-2xl mx-auto">
            Connect directly with your audience, monetize your content with $PATH tokens, and build your creator microplatform
          </p>
          
          <div className="flex flex-col sm:flex-row gap-4 justify-center mb-12">
            <button className="bg-green-500 hover:bg-green-600 text-black px-8 py-4 rounded-full text-lg font-semibold">
              Join Waitlist
            </button>
            <button 
              onClick={() => setCurrentPage('feed')}
              className="border border-green-500 text-green-500 hover:bg-green-500 hover:text-black px-8 py-4 rounded-full text-lg font-semibold"
            >
              Explore Creators
            </button>
          </div>
        </div>
      </div>

      {/* Features */}
      <div className="py-16 px-4 bg-gray-900">
        <div className="max-w-6xl mx-auto">
          <h2 className="text-3xl font-bold text-center mb-12">Why Choose PATH?</h2>
          
          <div className="grid md:grid-cols-3 gap-8">
            <div className="text-center p-6">
              <div className="w-16 h-16 bg-green-500/20 rounded-full flex items-center justify-center mx-auto mb-4">
                <Coins className="text-green-500" size={32} />
              </div>
              <h3 className="text-xl font-semibold mb-3">Token-Powered Economy</h3>
              <p className="text-gray-400">Earn and spend $PATH tokens for exclusive content and creator support</p>
            </div>
            
            <div className="text-center p-6">
              <div className="w-16 h-16 bg-green-500/20 rounded-full flex items-center justify-center mx-auto mb-4">
                <Lock className="text-green-500" size={32} />
              </div>
              <h3 className="text-xl font-semibold mb-3">Token-Gated Content</h3>
              <p className="text-gray-400">Access premium content and exclusive communities with your tokens</p>
            </div>
            
            <div className="text-center p-6">
              <div className="w-16 h-16 bg-green-500/20 rounded-full flex items-center justify-center mx-auto mb-4">
                <Users className="text-green-500" size={32} />
              </div>
              <h3 className="text-xl font-semibold mb-3">Direct Creator Support</h3>
              <p className="text-gray-400">Support your favorite creators directly with seamless tipping</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  );

  const FeedPage = () => (
    <div className="min-h-screen bg-black text-white">
      <NavBar />
      
      <div className="flex">
        <Sidebar currentPage={currentPage} setCurrentPage={setCurrentPage} />
        
        <div className="flex-1 max-w-2xl mx-auto px-4 py-6">
          <div className="flex items-center justify-between mb-6">
            <h1 className="text-2xl font-bold">Trending Creators</h1>
            <button className="text-green-500 hover:text-green-400 flex items-center space-x-1">
              <span>View All</span>
              <ChevronRight size={16} />
            </button>
          </div>

          {/* Post Feed */}
          <div className="space-y-6">
            {[1, 2, 3].map((post) => (
              <div key={post} className="bg-gray-900 rounded-lg border border-gray-800 p-6">
                <div className="flex items-center space-x-3 mb-4">
                  <div className="w-10 h-10 bg-green-500 rounded-full flex items-center justify-center">
                    <User className="text-black" size={20} />
                  </div>
                  <div>
                    <h3 className="font-semibold">Creator {post}</h3>
                    <p className="text-sm text-gray-400">@creator{post}</p>
                  </div>
                  <div className="ml-auto flex items-center space-x-2">
                    <Star className="text-yellow-500" size={16} />
                    <span className="text-sm text-gray-400">Premium</span>
                  </div>
                </div>
                
                <p className="text-gray-300 mb-4">
                  Check out my latest content! Token holders get exclusive access to behind-the-scenes footage.
                </p>
                
                <div className="flex items-center justify-between">
                  <div className="flex items-center space-x-4">
                    <button className="flex items-center space-x-2 text-gray-400 hover:text-red-500">
                      <Heart size={20} />
                      <span>{12 * post}</span>
                    </button>
                    <button className="flex items-center space-x-2 text-gray-400 hover:text-blue-500">
                      <MessageCircle size={20} />
                      <span>{5 * post}</span>
                    </button>
                    <button className="text-gray-400 hover:text-green-500">
                      <Share size={20} />
                    </button>
                  </div>
                  
                  <button className="bg-green-500 hover:bg-green-600 text-black px-4 py-2 rounded-full text-sm font-medium">
                    Tip $PATH
                  </button>
                </div>
              </div>
            ))}
          </div>
        </div>
      </div>
      
      <MobileNav currentPage={currentPage} setCurrentPage={setCurrentPage} />
    </div>
  );

  const CreatorProfilePage = () => (
    <div className="min-h-screen bg-black text-white">
      <NavBar />
      
      <div className="flex">
        <Sidebar currentPage={currentPage} setCurrentPage={setCurrentPage} />
        
        <div className="flex-1 px-4 py-6">
          <div className="max-w-4xl mx-auto">
            {/* Profile Header */}
            <div className="bg-gray-900 rounded-lg border border-gray-800 p-6 mb-6">
              <div className="flex flex-col md:flex-row items-start md:items-center space-y-4 md:space-y-0 md:space-x-6">
                <div className="w-24 h-24 bg-green-500 rounded-full flex items-center justify-center">
                  <User className="text-black" size={40} />
                </div>
                
                <div className="flex-1">
                  <div className="flex items-center space-x-3 mb-2">
                    <h1 className="text-3xl font-bold">Sarah Chen</h1>
                    <Star className="text-yellow-500" size={24} />
                  </div>
                  <p className="text-gray-400 mb-4">@sarahcreates</p>
                  <p className="text-gray-300 mb-4">
                    Digital artist & NFT creator. Sharing my journey in Web3 and exclusive tutorials for token holders.
                  </p>
                  
                  <div className="flex items-center space-x-4 text-sm text-gray-400">
                    <span>2.5K Followers</span>
                    <span>150 Posts</span>
                    <span>Member since 2024</span>
                  </div>
                </div>
                
                <div className="flex flex-col space-y-2">
                  <button className="bg-green-500 hover:bg-green-600 text-black px-6 py-2 rounded-full font-medium">
                    Follow
                  </button>
                  <button className="border border-green-500 text-green-500 hover:bg-green-500 hover:text-black px-6 py-2 rounded-full font-medium">
                    Tip $PATH
                  </button>
                </div>
              </div>
            </div>

            {/* Content Tabs */}
            <div className="flex space-x-6 mb-6 border-b border-gray-800">
              <button className="pb-2 border-b-2 border-green-500 text-green-500 font-medium">
                Posts
              </button>
              <button className="pb-2 text-gray-400 hover:text-white">
                Premium Content
              </button>
              <button className="pb-2 text-gray-400 hover:text-white">
                About
              </button>
            </div>

            {/* Content Grid */}
            <div className="grid md:grid-cols-2 gap-6">
              {[1, 2, 3, 4].map((item) => (
                <div key={item} className="bg-gray-900 rounded-lg border border-gray-800 p-4">
                  <div className="aspect-video bg-gray-800 rounded-lg mb-4 flex items-center justify-center">
                    {item % 2 === 0 ? (
                      <div className="flex items-center space-x-2 text-yellow-500">
                        <Lock size={20} />
                        <span>Premium Content</span>
                      </div>
                    ) : (
                      <span className="text-gray-500">Content Preview</span>
                    )}
                  </div>
                  
                  <h3 className="font-semibold mb-2">Tutorial {item}: Advanced Techniques</h3>
                  <p className="text-sm text-gray-400 mb-3">
                    Learn the secrets behind my latest NFT collection...
                  </p>
                  
                  <div className="flex items-center justify-between">
                    <span className="text-xs text-gray-500">2 days ago</span>
                    {item % 2 === 0 && (
                      <span className="text-xs bg-yellow-500/20 text-yellow-500 px-2 py-1 rounded-full">
                        50 $PATH
                      </span>
                    )}
                  </div>
                </div>
              ))}
            </div>
          </div>
        </div>
      </div>
      
      <MobileNav currentPage={currentPage} setCurrentPage={setCurrentPage} />
    </div>
  );

  const TokenDashboard = () => (
    <div className="min-h-screen bg-black text-white">
      <NavBar />
      
      <div className="flex">
        <Sidebar currentPage={currentPage} setCurrentPage={setCurrentPage} />
        
        <div className="flex-1 px-4 py-6">
          <div className="max-w-6xl mx-auto">
            <h1 className="text-3xl font-bold mb-8">Token Dashboard</h1>
            
            {/* Balance Cards */}
            <div className="grid md:grid-cols-3 gap-6 mb-8">
              <div className="bg-gray-900 rounded-lg border border-gray-800 p-6">
                <div className="flex items-center justify-between mb-4">
                  <h3 className="text-lg font-semibold">$PATH Balance</h3>
                  <Coins className="text-green-500" size={24} />
                </div>
                <p className="text-3xl font-bold text-green-500 mb-2">1,250</p>
                <p className="text-sm text-gray-400">≈ $125.00 USD</p>
              </div>
              
              <div className="bg-gray-900 rounded-lg border border-gray-800 p-6">
                <div className="flex items-center justify-between mb-4">
                  <h3 className="text-lg font-semibold">Staked $PATH</h3>
                  <Star className="text-yellow-500" size={24} />
                </div>
                <p className="text-3xl font-bold text-yellow-500 mb-2">500</p>
                <p className="text-sm text-gray-400">Earning 5% APY</p>
              </div>
              
              <div className="bg-gray-900 rounded-lg border border-gray-800 p-6">
                <div className="flex items-center justify-between mb-4">
                  <h3 className="text-lg font-semibold">Rewards Earned</h3>
                  <TrendingUp className="text-blue-500" size={24} />
                </div>
                <p className="text-3xl font-bold text-blue-500 mb-2">75</p>
                <p className="text-sm text-gray-400">This month</p>
              </div>
            </div>

            {/* Actions */}
            <div className="grid md:grid-cols-2 gap-6 mb-8">
              <div className="bg-gray-900 rounded-lg border border-gray-800 p-6">
                <h3 className="text-xl font-semibold mb-4">Quick Actions</h3>
                <div className="space-y-3">
                  <button className="w-full bg-green-500 hover:bg-green-600 text-black py-3 rounded-lg font-medium">
                    Buy $PATH Tokens
                  </button>
                  <button className="w-full border border-green-500 text-green-500 hover:bg-green-500 hover:text-black py-3 rounded-lg font-medium">
                    Stake Tokens
                  </button>
                  <button className="w-full border border-gray-600 text-gray-300 hover:bg-gray-800 py-3 rounded-lg font-medium">
                    Send to Friend
                  </button>
                </div>
              </div>
              
              <div className="bg-gray-900 rounded-lg border border-gray-800 p-6">
                <h3 className="text-xl font-semibold mb-4">Recent Transactions</h3>
                <div className="space-y-3">
                  {[
                    { type: 'Received', amount: '+50', from: 'Sarah Chen tip' },
                    { type: 'Spent', amount: '-25', from: 'Premium content' },
                    { type: 'Earned', amount: '+10', from: 'Staking rewards' }
                  ].map((tx, i) => (
                    <div key={i} className="flex items-center justify-between py-2 border-b border-gray-800 last:border-b-0">
                      <div>
                        <p className="font-medium">{tx.type}</p>
                        <p className="text-sm text-gray-400">{tx.from}</p>
                      </div>
                      <span className={`font-semibold ${tx.amount.startsWith('+') ? 'text-green-500' : 'text-red-500'}`}>
                        {tx.amount} $PATH
                      </span>
                    </div>
                  ))}
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <MobileNav currentPage={currentPage} setCurrentPage={setCurrentPage} />
    </div>
  );

  const CreatorOnboarding = () => (
    <div className="min-h-screen bg-black text-white">
      <NavBar />
      
      <div className="flex">
        <Sidebar currentPage={currentPage} setCurrentPage={setCurrentPage} />
        
        <div className="flex-1 px-4 py-6">
          <div className="max-w-2xl mx-auto">
            <div className="text-center mb-8">
              <h1 className="text-3xl font-bold mb-4">Welcome to PATH</h1>
              <p className="text-gray-400">Let's set up your creator profile in just a few steps</p>
            </div>

            <div className="bg-gray-900 rounded-lg border border-gray-800 p-6">
              {/* Progress Steps */}
              <div className="flex items-center justify-between mb-8">
                {[1, 2, 3, 4].map((step) => (
                  <div key={step} className="flex items-center">
                    <div className={`w-8 h-8 rounded-full flex items-center justify-center ${
                      step <= 2 ? 'bg-green-500 text-black' : 'bg-gray-700 text-gray-400'
                    }`}>
                      {step}
                    </div>
                    {step < 4 && <div className={`w-16 h-0.5 ${step < 2 ? 'bg-green-500' : 'bg-gray-700'}`} />}
                  </div>
                ))}
              </div>

              {/* Form Fields */}
              <div className="space-y-6">
                <div>
                  <label className="block text-sm font-medium mb-2">Profile Picture</label>
                  <div className="flex items-center space-x-4">
                    <div className="w-16 h-16 bg-gray-700 rounded-full flex items-center justify-center">
                      <User className="text-gray-400" size={24} />
                    </div>
                    <button className="bg-green-500 hover:bg-green-600 text-black px-4 py-2 rounded-lg font-medium">
                      Upload Image
                    </button>
                  </div>
                </div>

                <div>
                  <label className="block text-sm font-medium mb-2">Display Name</label>
                  <input 
                    type="text" 
                    placeholder="Your creator name"
                    className="w-full bg-gray-800 border border-gray-700 rounded-lg px-4 py-3 text-white placeholder-gray-400 focus:border-green-500 focus:outline-none"
                  />
                </div>

                <div>
                  <label className="block text-sm font-medium mb-2">Username</label>
                  <div className="relative">
                    <span className="absolute left-3 top-3 text-gray-400">@</span>
                    <input 
                      type="text" 
                      placeholder="username"
                      className="w-full bg-gray-800 border border-gray-700 rounded-lg pl-8 pr-4 py-3 text-white placeholder-gray-400 focus:border-green-500 focus:outline-none"
                    />
                  </div>
                </div>

                <div>
                  <label className="block text-sm font-medium mb-2">Bio</label>
                  <textarea 
                    placeholder="Tell your audience about yourself..."
                    rows={4}
                    className="w-full bg-gray-800 border border-gray-700 rounded-lg px-4 py-3 text-white placeholder-gray-400 focus:border-green-500 focus:outline-none resize-none"
                  />
                </div>

                <div className="bg-gray-800 border border-gray-700 rounded-lg p-4">
                  <div className="flex items-center justify-between mb-2">
                    <span className="font-medium">Wallet Connection</span>
                    {isWalletConnected ? (
                      <span className="text-green-500 text-sm">✓ Connected</span>
                    ) : (
                      <span className="text-red-500 text-sm">Not connected</span>
                    )}
                  </div>
                  <p className="text-sm text-gray-400 mb-3">
                    Connect your Solana wallet to receive $PATH tokens and tips from supporters
                  </p>
                  {!isWalletConnected && (
                    <button 
                      onClick={() => setIsWalletConnected(true)}
                      className="bg-green-500 hover:bg-green-600 text-black px-4 py-2 rounded-lg font-medium"
                    >
                      Connect Solana Wallet
                    </button>
                  )}
                </div>

                <div className="flex space-x-4 pt-4">
                  <button className="flex-1 border border-gray-600 text-gray-300 hover:bg-gray-800 py-3 rounded-lg font-medium">
                    Back
                  </button>
                  <button className="flex-1 bg-green-500 hover:bg-green-600 text-black py-3 rounded-lg font-medium">
                    Continue
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <MobileNav currentPage={currentPage} setCurrentPage={setCurrentPage} />
    </div>
  );

  const SettingsPage = () => (
    <div className="min-h-screen bg-black text-white">
      <NavBar />
      
      <div className="flex">
        <Sidebar currentPage={currentPage} setCurrentPage={setCurrentPage} />
        
        <div className="flex-1 px-4 py-6">
          <div className="max-w-4xl mx-auto">
            <h1 className="text-3xl font-bold mb-8">Settings</h1>
            
            <div className="grid md:grid-cols-2 gap-6">
              {/* Profile Settings */}
              <div className="bg-gray-900 rounded-lg border border-gray-800 p-6">
                <h3 className="text-xl font-semibold mb-4">Profile Settings</h3>
                <div className="space-y-4">
                  <button className="w-full flex items-center justify-between p-3 bg-gray-800 rounded-lg hover:bg-gray-700">
                    <div className="flex items-center space-x-3">
                      <Edit3 size={20} />
                      <span>Edit Profile</span>
                    </div>
                    <ChevronRight size={20} />
                  </button>
                  
                  <button className="w-full flex items-center justify-between p-3 bg-gray-800 rounded-lg hover:bg-gray-700">
                    <div className="flex items-center space-x-3">
                      <Lock size={20} />
                      <span>Privacy Settings</span>
                    </div>
                    <ChevronRight size={20} />
                  </button>
                  
                  <button className="w-full flex items-center justify-between p-3 bg-gray-800 rounded-lg hover:bg-gray-700">
                    <div className="flex items-center space-x-3">
                      <Bell size={20} />
                      <span>Notifications</span>
                    </div>
                    <ChevronRight size={20} />
                  </button>
                </div>
              </div>

              {/* Wallet Settings */}
              <div className="bg-gray-900 rounded-lg border border-gray-800 p-6">
                <h3 className="text-xl font-semibold mb-4">Wallet & Tokens</h3>
                <div className="space-y-4">
                  <button className="w-full flex items-center justify-between p-3 bg-gray-800 rounded-lg hover:bg-gray-700">
                    <div className="flex items-center space-x-3">
                      <Wallet size={20} />
                      <span>Manage Wallets</span>
                    </div>
                    <ChevronRight size={20} />
                  </button>
                  
                  <button className="w-full flex items-center justify-between p-3 bg-gray-800 rounded-lg hover:bg-gray-700">
                    <div className="flex items-center space-x-3">
                      <Coins size={20} />
                      <span>Token Settings</span>
                    </div>
                    <ChevronRight size={20} />
                  </button>
                  
                  <button className="w-full flex items-center justify-between p-3 bg-gray-800 rounded-lg hover:bg-gray-700">
                    <div className="flex items-center space-x-3">
                      <Star size={20} />
                      <span>Staking Preferences</span>
                    </div>
                    <ChevronRight size={20} />
                  </button>
                </div>
              </div>

              {/* Creator Tools */}
              <div className="bg-gray-900 rounded-lg border border-gray-800 p-6">
                <h3 className="text-xl font-semibold mb-4">Creator Tools</h3>
                <div className="space-y-4">
                  <button className="w-full flex items-center justify-between p-3 bg-gray-800 rounded-lg hover:bg-gray-700">
                    <div className="flex items-center space-x-3">
                      <Users size={20} />
                      <span>Audience Analytics</span>
                    </div>
                    <ChevronRight size={20} />
                  </button>
                  
                  <button className="w-full flex items-center justify-between p-3 bg-gray-800 rounded-lg hover:bg-gray-700">
                    <div className="flex items-center space-x-3">
                      <TrendingUp size={20} />
                      <span>Revenue Dashboard</span>
                    </div>
                    <ChevronRight size={20} />
                  </button>
                </div>
              </div>

              {/* Support */}
              <div className="bg-gray-900 rounded-lg border border-gray-800 p-6">
                <h3 className="text-xl font-semibold mb-4">Support & Help</h3>
                <div className="space-y-4">
                  <button className="w-full flex items-center justify-between p-3 bg-gray-800 rounded-lg hover:bg-gray-700">
                    <div className="flex items-center space-x-3">
                      <ExternalLink size={20} />
                      <span>Help Center</span>
                    </div>
                    <ChevronRight size={20} />
                  </button>
                  
                  <button className="w-full flex items-center justify-between p-3 bg-gray-800 rounded-lg hover:bg-gray-700">
                    <div className="flex items-center space-x-3">
                      <MessageCircle size={20} />
                      <span>Contact Support</span>
                    </div>
                    <ChevronRight size={20} />
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <MobileNav currentPage={currentPage} setCurrentPage={setCurrentPage} />
    </div>
  );

  const renderCurrentPage = () => {
    switch(currentPage) {
      case 'landing':
        return <LandingPage />;
      case 'feed':
        return <FeedPage />;
      case 'profile':
        return <CreatorProfilePage />;
      case 'dashboard':
        return <TokenDashboard />;
      case 'onboarding':
        return <CreatorOnboarding />;
      case 'settings':
        return <SettingsPage />;
      default:
        return <LandingPage />;
    }
  };

  return (
    <div className="min-h-screen bg-black">
      {renderCurrentPage()}
    </div>
  );
};

export default WireframeApp;
