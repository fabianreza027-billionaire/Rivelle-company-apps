import React, { useState, useEffect } from 'react';
import { ShoppingCart, Search, User, Menu, X, Star, Heart, Infinity } from 'lucide-react';

const App = () => {
  const [isMenuOpen, setIsMenuOpen] = useState(false);
  const [cartItems, setCartItems] = useState([]);
  const [selectedCategory, setSelectedCategory] = useState('all');

  // Mock product data
  const products = [
    {
      id: 1,
      name: "Luxury Silk Scarf",
      price: 89.99,
      originalPrice: 120.00,
      image: "https://placehold.co/400x500/1C1C1C/D4AF37?text=Luxury+Scarf",
      category: "accessories",
      rating: 4.8,
      reviews: 124
    },
    {
      id: 2,
      name: "Premium Leather Handbag",
      price: 299.99,
      originalPrice: 399.00,
      image: "https://placehold.co/400x500/1C1C1C/D4AF37?text=Leather+Bag",
      category: "bags",
      rating: 4.9,
      reviews: 89
    },
    {
      id: 3,
      name: "Elegant Evening Gown",
      price: 199.99,
      originalPrice: 280.00,
      image: "https://placehold.co/400x500/1C1C1C/D4AF37?text=Evening+Gown",
      category: "clothing",
      rating: 4.7,
      reviews: 156
    },
    {
      id: 4,
      name: "Designer Sunglasses",
      price: 149.99,
      originalPrice: 199.00,
      image: "https://placehold.co/400x500/1C1C1C/D4AF37?text=Sunglasses",
      category: "accessories",
      rating: 4.6,
      reviews: 203
    },
    {
      id: 5,
      name: "Classic Wool Coat",
      price: 349.99,
      originalPrice: 450.00,
      image: "https://placehold.co/400x500/1C1C1C/D4AF37?text=Wool+Coat",
      category: "clothing",
      rating: 4.9,
      reviews: 78
    },
    {
      id: 6,
      name: "Luxury Watch Collection",
      price: 599.99,
      originalPrice: 799.00,
      image: "https://placehold.co/400x500/1C1C1C/D4AF37?text=Luxury+Watch",
      category: "accessories",
      rating: 4.8,
      reviews: 142
    }
  ];

  const categories = [
    { id: 'all', name: 'All Products' },
    { id: 'clothing', name: 'Clothing' },
    { id: 'bags', name: 'Bags' },
    { id: 'accessories', name: 'Accessories' },
    { id: 'jewelry', name: 'Jewelry' }
  ];

  const filteredProducts = selectedCategory === 'all' 
    ? products 
    : products.filter(product => product.category === selectedCategory);

  const addToCart = (product) => {
    setCartItems(prev => {
      const existing = prev.find(item => item.id === product.id);
      if (existing) {
        return prev.map(item => 
          item.id === product.id 
            ? { ...item, quantity: item.quantity + 1 }
            : item
        );
      }
      return [...prev, { ...product, quantity: 1 }];
    });
  };

  const getTotalItems = () => {
    return cartItems.reduce((total, item) => total + item.quantity, 0);
  };

  return (
    <div className="min-h-screen bg-white">
      {/* Header */}
      <header className="bg-[#1C1C1C] text-white sticky top-0 z-50">
        <div className="container mx-auto px-4">
          <div className="flex items-center justify-between h-16">
            {/* Logo */}
            <div className="flex items-center space-x-2">
              <Infinity className="h-8 w-8 text-[#D4AF37]" />
              <span className="text-2xl font-bold tracking-wider">RIVELLE</span>
            </div>

            {/* Desktop Navigation */}
            <nav className="hidden md:flex space-x-8">
              {categories.map(category => (
                <button
                  key={category.id}
                  onClick={() => setSelectedCategory(category.id)}
                  className={`hover:text-[#D4AF37] transition-colors ${
                    selectedCategory === category.id ? 'text-[#D4AF37]' : ''
                  }`}
                >
                  {category.name}
                </button>
              ))}
            </nav>

            {/* Icons */}
            <div className="flex items-center space-x-4">
              <Search className="h-5 w-5 hover:text-[#D4AF37] cursor-pointer transition-colors" />
              <User className="h-5 w-5 hover:text-[#D4AF37] cursor-pointer transition-colors" />
              <div className="relative">
                <ShoppingCart className="h-5 w-5 hover:text-[#D4AF37] cursor-pointer transition-colors" />
                {getTotalItems() > 0 && (
                  <span className="absolute -top-2 -right-2 bg-[#D4AF37] text-[#1C1C1C] text-xs rounded-full h-5 w-5 flex items-center justify-center">
                    {getTotalItems()}
                  </span>
                )}
              </div>
              <button 
                className="md:hidden"
                onClick={() => setIsMenuOpen(!isMenuOpen)}
              >
                {isMenuOpen ? <X className="h-6 w-6" /> : <Menu className="h-6 w-6" />}
              </button>
            </div>
          </div>

          {/* Mobile Navigation */}
          {isMenuOpen && (
            <div className="md:hidden py-4 border-t border-gray-700">
              <nav className="flex flex-col space-y-3">
                {categories.map(category => (
                  <button
                    key={category.id}
                    onClick={() => {
                      setSelectedCategory(category.id);
                      setIsMenuOpen(false);
                    }}
                    className={`text-left hover:text-[#D4AF37] transition-colors ${
                      selectedCategory === category.id ? 'text-[#D4AF37]' : ''
                    }`}
                  >
                    {category.name}
                  </button>
                ))}
              </nav>
            </div>
          )}
        </div>
      </header>

      {/* Hero Section */}
      <section className="relative bg-gradient-to-r from-[#1C1C1C] to-black text-white">
        <div className="container mx-auto px-4 py-20 md:py-32">
          <div className="max-w-2xl">
            <h1 className="text-4xl md:text-6xl font-bold mb-6 leading-tight">
              Timeless Elegance, Modern Luxury
            </h1>
            <p className="text-xl mb-8 text-gray-300">
              Discover our curated collection of premium fashion pieces designed for the modern individual.
            </p>
            <button className="bg-[#D4AF37] text-[#1C1C1C] px-8 py-3 text-lg font-semibold hover:bg-opacity-90 transition-all transform hover:scale-105">
              Shop Collection
            </button>
          </div>
        </div>
      </section>

      {/* Featured Categories */}
      <section className="py-16 bg-gray-50">
        <div className="container mx-auto px-4">
          <h2 className="text-3xl font-bold text-center mb-12 text-[#1C1C1C]">Shop by Category</h2>
          <div className="grid grid-cols-2 md:grid-cols-4 gap-6">
            {categories.slice(1).map((category, index) => (
              <div 
                key={category.id}
                className="relative overflow-hidden rounded-lg group cursor-pointer"
                onClick={() => setSelectedCategory(category.id)}
              >
                <img 
                  src={`https://placehold.co/300x400/1C1C1C/D4AF37?text=${category.name}`}
                  alt={category.name}
                  className="w-full h-64 object-cover transition-transform group-hover:scale-110"
                />
                <div className="absolute inset-0 bg-black bg-opacity-40 flex items-center justify-center">
                  <h3 className="text-white text-xl font-semibold">{category.name}</h3>
                </div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Products Section */}
      <section className="py-16">
        <div className="container mx-auto px-4">
          <div className="flex justify-between items-center mb-8">
            <h2 className="text-3xl font-bold text-[#1C1C1C]">
              {selectedCategory === 'all' ? 'Featured Products' : `${categories.find(c => c.id === selectedCategory)?.name}`}
            </h2>
            <div className="text-sm text-gray-600">
              {filteredProducts.length} products
            </div>
          </div>

          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            {filteredProducts.map(product => (
              <div key={product.id} className="group">
                <div className="relative overflow-hidden rounded-lg mb-4">
                  <img 
                    src={product.image}
                    alt={product.name}
                    className="w-full h-80 object-cover transition-transform group-hover:scale-105"
                  />
                  <div className="absolute top-4 right-4">
                    <Heart className="h-6 w-6 text-white opacity-70 hover:opacity-100 cursor-pointer transition-opacity" />
                  </div>
                  <div className="absolute inset-0 bg-black bg-opacity-0 group-hover:bg-opacity-20 transition-all duration-300 flex items-center justify-center">
                    <button 
                      onClick={() => addToCart(product)}
                      className="bg-[#D4AF37] text-[#1C1C1C] px-6 py-2 font-semibold opacity-0 group-hover:opacity-100 transform translate-y-4 group-hover:translate-y-0 transition-all duration-300"
                    >
                      Add to Cart
                    </button>
                  </div>
                </div>
                <div className="space-y-2">
                  <h3 className="font-semibold text-lg text-[#1C1C1C]">{product.name}</h3>
                  <div className="flex items-center space-x-2">
                    <div className="flex items-center">
                      {[...Array(5)].map((_, i) => (
                        <Star 
                          key={i} 
                          className={`h-4 w-4 ${i < Math.floor(product.rating) ? 'text-yellow-400 fill-current' : 'text-gray-300'}`} 
                        />
                      ))}
                    </div>
                    <span className="text-sm text-gray-600">({product.reviews})</span>
                  </div>
                  <div className="flex items-center space-x-2">
                    <span className="text-xl font-bold text-[#1C1C1C]">${product.price}</span>
                    <span className="text-sm text-gray-500 line-through">${product.originalPrice}</span>
                    <span className="text-sm text-red-500">-{Math.round((1 - product.price/product.originalPrice) * 100)}%</span>
                  </div>
                </div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* About Section */}
      <section className="py-16 bg-[#1C1C1C] text-white">
        <div className="container mx-auto px-4">
          <div className="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
            <div>
              <h2 className="text-3xl font-bold mb-6">The Rivelle Heritage</h2>
              <p className="text-gray-300 mb-6 leading-relaxed">
                Founded on the principles of timeless elegance and modern sophistication, Rivelle brings you 
                curated luxury pieces that transcend trends. Our commitment to quality craftsmanship and 
                sustainable practices ensures that every item in our collection tells a story of heritage 
                and innovation.
              </p>
              <p className="text-gray-300 mb-8 leading-relaxed">
                Each piece is carefully selected to embody the perfect balance between classic design and 
                contemporary style, ensuring you make a statement that lasts beyond seasons.
              </p>
              <button className="border border-[#D4AF37] text-[#D4AF37] px-8 py-3 font-semibold hover:bg-[#D4AF37] hover:text-[#1C1C1C] transition-all">
                Discover Our Story
              </button>
            </div>
            <div className="relative">
              <img 
                src="https://placehold.co/600x400/1C1C1C/D4AF37?text=Rivelle+Heritage"
                alt="Rivelle Heritage"
                className="rounded-lg"
              />
              <div className="absolute -bottom-6 -right-6 bg-[#D4AF37] text-[#1C1C1C] p-6 rounded-lg">
                <div className="text-3xl font-bold">Since 2023</div>
                <div className="text-sm">Crafting Excellence</div>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="bg-black text-white py-12">
        <div className="container mx-auto px-4">
          <div className="grid grid-cols-1 md:grid-cols-4 gap-8">
            <div>
              <div className="flex items-center space-x-2 mb-4">
                <Infinity className="h-8 w-8 text-[#D4AF37]" />
                <span className="text-2xl font-bold">RIVELLE</span>
              </div>
              <p className="text-gray-400 mb-4">
                Timeless elegance meets modern luxury in every piece we curate for you.
              </p>
              <div className="flex space-x-4">
                <div className="w-8 h-8 bg-gray-800 rounded-full flex items-center justify-center cursor-pointer hover:bg-[#D4AF37] transition-colors">
                  <span className="text-xs">f</span>
                </div>
                <div className="w-8 h-8 bg-gray-800 rounded-full flex items-center justify-center cursor-pointer hover:bg-[#D4AF37] transition-colors">
                  <span className="text-xs">ig</span>
                </div>
                <div className="w-8 h-8 bg-gray-800 rounded-full flex items-center justify-center cursor-pointer hover:bg-[#D4AF37] transition-colors">
                  <span className="text-xs">t</span>
                </div>
              </div>
            </div>
            
            <div>
              <h3 className="text-lg font-semibold mb-4">Shop</h3>
              <ul className="space-y-2 text-gray-400">
                <li className="hover:text-[#D4AF37] cursor-pointer transition-colors">New Arrivals</li>
                <li className="hover:text-[#D4AF37] cursor-pointer transition-colors">Best Sellers</li>
                <li className="hover:text-[#D4AF37] cursor-pointer transition-colors">Sale</li>
                <li className="hover:text-[#D4AF37] cursor-pointer transition-colors">Collections</li>
              </ul>
            </div>
            
            <div>
              <h3 className="text-lg font-semibold mb-4">Support</h3>
              <ul className="space-y-2 text-gray-400">
                <li className="hover:text-[#D4AF37] cursor-pointer transition-colors">Contact Us</li>
                <li className="hover:text-[#D4AF37] cursor-pointer transition-colors">Shipping Info</li>
                <li className="hover:text-[#D4AF37] cursor-pointer transition-colors">Returns</li>
                <li className="hover:text-[#D4AF37] cursor-pointer transition-colors">Size Guide</li>
              </ul>
            </div>
            
            <div>
              <h3 className="text-lg font-semibold mb-4">Newsletter</h3>
              <p className="text-gray-400 mb-4">
                Subscribe to receive updates, access to exclusive deals, and more.
              </p>
              <div className="flex">
                <input 
                  type="email" 
                  placeholder="Your email" 
                  className="bg-gray-800 text-white px-4 py-2 w-full rounded-l focus:outline-none"
                />
                <button className="bg-[#D4AF37] text-[#1C1C1C] px-4 py-2 rounded-r font-semibold hover:bg-opacity-90 transition-colors">
                  Join
                </button>
              </div>
            </div>
          </div>
          
          <div className="border-t border-gray-800 mt-12 pt-8 text-center text-gray-400">
            <p>&copy; 2023 Rivelle. All rights reserved. Crafted with elegance.</p>
          </div>
        </div>
      </footer>
    </div>
  );
};

export default App;
