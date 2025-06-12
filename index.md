<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="title" content="Southwest Short Term Stays | Luxury Airbnb Management & Real Estate">
  <meta name="description" content="Southwest Short Term Stays offers premier short-term rental management, real estate sales, and luxury home renovations in West Chester, Germantown, Norris Lake, and Red River Gorge. Maximize your property's value with our local expertise.">
  <meta name="keywords" content="Airbnb management, short-term rentals, West Chester real estate, Norris Lake homes, Red River Gorge cabins">
  <title>Southwest Short Term Stays | Luxury Airbnb Management & Real Estate</title>
  <script src="https://cdn.jsdelivr.net/npm/react@18.2.0/umd/react.production.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/react-dom@18.2.0/umd/react-dom.production.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/@babel/standalone@7.20.15/babel.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/emailjs-com@3.2.0/dist/email.min.js"></script>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
  <div id="root"></div>
  <script type="text/babel">
    // Initialize EmailJS with your public key
    // TODO: Replace 'YOUR_EMAILJS_PUBLIC_KEY' with your EmailJS User ID (from EmailJS dashboard > Account > API Keys)
    emailjs.init("YOUR_EMAILJS_PUBLIC_KEY");

    // Main App Component
    const App = () => {
      const [isModalOpen, setIsModalOpen] = React.useState(false);
      const [formData, setFormData] = React.useState({ name: '', email: '', phone: '', message: '' });
      const [error, setError] = React.useState('');

      // Handle modal toggle
      const toggleModal = () => {
        setIsModalOpen(!isModalOpen);
        setError('');
      };

      // Handle input changes
      const handleInputChange = (e) => {
        const { name, value } = e.target;
        setFormData({ ...formData, [name]: value });
        setError('');
      };

      // Validate email format
      const isValidEmail = (email) => {
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        return emailRegex.test(email);
      };

      // Handle form submission (sends email via EmailJS)
      const handleSubmit = (e) => {
        e.preventDefault();
        if (!formData.name || !formData.email) {
          setError('Please fill out Name and Email fields');
          return;
        }
        if (!isValidEmail(formData.email)) {
          setError('Please enter a valid email address');
          return;
        }
        // TODO: Replace 'YOUR_SERVICE_ID' and 'YOUR_TEMPLATE_ID' with your EmailJS Service ID and Template ID
        emailjs.send('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', {
          from_name: formData.name,
          from_email: formData.email,
          phone: formData.phone,
          message: formData.message,
          to_email: 'joey.brown@cbishome.com'
        }, 'YOUR_EMAILJS_PUBLIC_KEY')
          .then((response) => {
            console.log('Email sent successfully:', response);
            alert('Thank you! Your request has been sent to Southwest Short Term Stays.');
            setFormData({ name: '', email: '', phone: '', message: '' });
            toggleModal();
          }, (error) => {
            console.error('Email sending failed:', error);
            setError(`Failed to send request: ${error.text || 'Unknown error. Please try again.'}`);
          });
      };

      // Smooth scroll to section
      const scrollToSection = (id) => {
        document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' });
      };

      return (
        <div className="font-sans text-gray-800">
          {/* Navigation Bar */}
          <nav className="bg-blue-900 text-white sticky top-0 z-50 shadow-lg">
            <div className="container mx-auto px-4 py-4 flex justify-between items-center">
              <h1 className="text-2xl font-bold font-[Montserrat]">
                Southwest Short Term Stays
              </h1>
              <ul className="flex space-x-6">
                {['Home', 'About', 'Services', 'Locations', 'Testimonials', 'Contact'].map((item) => (
                  <li key={item}>
                    <button
                      onClick={() => scrollToSection(item.toLowerCase())}
                      className="hover:text-yellow-400 transition-colors"
                      aria-label={`Navigate to ${item} section`}
                    >
                      {item}
                    </button>
                  </li>
                ))}
              </ul>
            </div>
          </nav>

          {/* Hero Section */}
          <section id="home" className="relative">
            <img
              src="https://images.unsplash.com/photo-1613977257363-707ba9348227?ixlib=rb-4.0.3&auto=format&fit=crop&w=1920&q=80"
              alt="Luxury lakefront Airbnb at Norris Lake"
              className="w-full h-[600px] object-cover"
            />
            <div className="absolute inset-0 bg-black bg-opacity-50 flex items-center justify-center">
              <div className="text-center text-white">
                <h1 className="text-4xl md:text-6xl font-bold font-[Montserrat] mb-4">
                  Turn Your Property into Profit
                </h1>
                <p className="text-xl md:text-2xl font-[Open Sans] mb-6">
                  Premier Short-Term Rental Management, Real Estate Sales, and Luxury Renovations
                </p>
                <button
                  onClick={toggleModal}
                  className="bg-yellow-400 text-blue-900 px-6 py-3 rounded-lg font-semibold hover:bg-yellow-500 transition-colors"
                  aria-label="Get your free rental income analysis"
                >
                  Get Your Free Rental Income Analysis
                </button>
              </div>
            </div>
          </section>

          {/* About Section */}
          <section id="about" className="py-16 bg-gray-100">
            <div className="container mx-auto px-4">
              <h2 className="text-3xl md:text-4xl font-bold font-[Montserrat] text-center mb-8">
                Welcome to Southwest Short Term Stays
              </h2>
              <div className="flex flex-col md:flex-row items-center">
                <div className="md:w-1/2 mb-6 md:mb-0">
                  <p className="text-lg font-[Open Sans] mb-4">
                    As a West Chester, Ohio native, I lead Southwest Short Term Stays with unmatched local expertise. Specializing in short-term rental management, real estate sales, and home renovations, I help homeowners and investors maximize property value and income. Trust us to deliver high-ROI solutions with a personal, professional touch.
                  </p>
                </div>
                <div className="md:w-1/2">
                  <div className="text-center text-gray-500">[Placeholder: Insert professional headshot of Joey Brown]</div>
                </div>
              </div>
            </div>
          </section>

          {/* Services Section */}
          <section id="services" className="py-16">
            <div className="container mx-auto px-4">
              <h2 className="text-3xl md:text-4xl font-bold font-[Montserrat] text-center mb-8">
                Our Premier Services
              </h2>
              <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
                <ServiceCard
                  title="Short-Term Rental Management"
                  description="Maximize your Airbnb or VRBO income by up to 30% with our full-service management: seamless bookings, guest communication, professional cleaning, and maintenance."
                  image="https://images.unsplash.com/photo-1613490493576-7fde63acd811?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80"
                  alt="Cozy Airbnb interior"
                />
                <ServiceCard
                  title="Real Estate Sales"
                  description="Buy or sell with confidence, leveraging our deep knowledge of West Chester, Germantown, and Norris Lake markets for stress-free transactions."
                  image="https://images.unsplash.com/photo-1600585154340-be6161a56a0c?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80"
                  alt="Modern home exterior"
                />
                <ServiceCard
                  title="Home Renovations"
                  description="Transform your property with luxury upgrades—open-concept designs, smart home technology, and energy-efficient systems—for up to 20% ROI."
                  image="https://images.unsplash.com/photo-1600607687920-4e2a09cf159d?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80"
                  alt="Renovated kitchen with quartz countertops"
                />
              </div>
            </div>
          </section>

          {/* Locations Section */}
          <section id="locations" className="py-16 bg-gray-100">
            <div className="container mx-auto px-4">
              <h2 className="text-3xl md:text-4xl font-bold font-[Montserrat] text-center mb-8">
                Featured Locations
              </h2>
              <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
                <LocationCard
                  title="Norris Lake, TN"
                  description="Crafting luxury lakefront homes, ideal for short-term rentals or vacation retreats. Limited lots—reserve yours today!"
                  image="https://images.unsplash.com/photo-1507525428034-b723cf961d3e?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80"
                  alt="Lakefront property at Norris Lake"
                />
                <LocationCard
                  title="West Chester, OH"
                  description="Remodeling a home with premium upgrades like quartz countertops and hardwood floors. See the transformation!"
                  image="https://images.unsplash.com/photo-1600585154526-990dced4db0d?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80"
                  alt="Modern home interior in West Chester"
                />
                <LocationCard
                  title="Germantown, OH"
                  description="Selling a move-in-ready bi-level home with a spacious lot, perfect for families or rental investors."
                  image="https://images.unsplash.com/photo-1600585154340-be6161a56a0c?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80"
                  alt="Bi-level home exterior in Germantown"
                />
                <LocationCard
                  title="Red River Gorge, KY"
                  description="Developing adventure-ready short-term rentals nestled in the heart of Red River Gorge, perfect for climbers, hikers, and nature lovers. Join our vision!"
                  image="https://images.unsplash.com/photo-1508739773434-c26b3d09e206?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80"
                  alt="Cabin in Red River Gorge"
                />
              </div>
              <div className="text-center mt-8">
                <button
                  onClick={toggleModal}
                  className="bg-yellow-400 text-blue-900 px-6 py-3 rounded-lg font-semibold hover:bg-yellow-500 transition-colors"
                  aria-label="Explore our listings"
                >
                  Explore Listings
                </button>
              </div>
            </div>
          </section>

          {/* Why Choose Us Section */}
          <section id="why-choose-us" className="py-16">
            <div className="container mx-auto px-4">
              <h2 className="text-3xl md:text-4xl font-bold font-[Montserrat] text-center mb-8">
                Why Partner with Us?
              </h2>
              <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div className="text-center">
                  <svg className="w-12 h-12 mx-auto mb-4 text-yellow-400" fill="currentColor" viewBox="0 0 20 20">
                    <path d="M10 2a8 8 0 100 16 8 8 0 000-16zm1 11H9v-2h2v2zm0-4H9V5h2v4z" />
                  </svg>
                  <h3 className="text-xl font-semibold font-[Montserrat] mb-2">West Chester Native</h3>
                  <p className="font-[Open Sans]">Born and raised here, I know the local market inside and out.</p>
                </div>
                <div className="text-center">
                  <svg className="w-12 h-12 mx-auto mb-4 text-yellow-400" fill="currentColor" viewBox="0 0 20 20">
                    <path d="M10 2a8 8 0 100 16 8 8 0 000-16zm1 11H9v-2h2v2zm0-4H9V5h2v4z" />
                  </svg>
                  <h3 className="text-xl font-semibold font-[Montserrat] mb-2">Proven ROI</h3>
                  <p className="font-[Open Sans]">Our rentals and renovations deliver top returns for property owners.</p>
                </div>
                <div className="text-center">
                  <svg className="w-12 h-12 mx-auto mb-4 text-yellow-400" fill="currentColor" viewBox="0 0 20 20">
                    <path d="M10 2a8 8 0 100 16 8 8 0 000-16zm1 11H9v-2h2v2zm0-4H9V5h2v4z" />
                  </svg>
                  <h3 className="text-xl font-semibold font-[Montserrat] mb-2">Seamless Experience</h3>
                  <p className="font-[Open Sans]">From rentals to sales to remodels, we manage every detail for you.</p>
                </div>
              </div>
            </div>
          </section>

          {/* Testimonials Section */}
          <section id="testimonials" className="py-16 bg-gray-100">
            <div className="container mx-auto px-4">
              <h2 className="text-3xl md:text-4xl font-bold font-[Montserrat] text-center mb-8">
                What Our Clients Say
              </h2>
              <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
                <TestimonialCard
                  quote="Working with Southwest Short Term Stays was a game-changer for my West Chester property! Their team turned my home into a top-performing Airbnb, earning me $3,800 a month with zero hassle. Their local expertise and seamless management made all the difference."
                  author="Emily R."
                  location="West Chester Homeowner"
                />
                <TestimonialCard
                  quote="I invested in a Red River Gorge rental with Southwest Short Term Stays, and I’m thrilled with the results. My cabin now brings in $4,000 a month, thanks to their expert booking strategies and adventure-focused marketing. Highly recommend!"
                  author="Mark T."
                  location="Red River Gorge Investor"
                />
                <TestimonialCard
                  quote="Southwest Short Term Stays transformed my Germantown property into a short-term rental goldmine, generating $3,500 monthly. Their renovation tips and hands-off management let me focus on my busy life while the income rolls in!"
                  author="Lisa M."
                  location="Germantown Property Owner"
                />
              </div>
            </div>
          </section>

          {/* Contact Section */}
          <section id="contact" className="py-16">
            <div className="container mx-auto px-4">
              <h2 className="text-3xl md:text-4xl font-bold font-[Montserrat] text-center mb-8">
                Contact Us
              </h2>
              <p className="text-lg font-[Open Sans] text-center mb-6">
                Call us today for a FREE Rental Income Analysis or Property Consultation! DM <a href="https://facebook.com/SouthwestShortTermStays" className="text-blue-600 hover:underline" target="_blank" rel="noopener noreferrer">@SouthwestShortTermStays</a> to schedule a tour or explore listings.
              </p>
              <div className="text-center mb-6">
                <p className="font-[Open Sans]"><strong>Southwest Short Term Stays</strong></p>
                <p className="font-[Open Sans]">Joey Brown 📞 <a href="tel:+15135717248" className="text-blue-600 hover:underline">(513) 571-7248</a></p>
                <p className="font-[Open Sans]">Caroline Higgs 📞 <a href="tel:+15138495502" className="text-blue-600 hover:underline">(513) 849-5502</a></p>
                <p className="font-[Open Sans]">📧 <a href="mailto:joey.brown@cbishome.com" className="text-blue-600 hover:underline">joey.brown@cbishome.com</a></p>
                <p className="font-[Open Sans]">📱 <a href="https://facebook.com/SouthwestShortTermStays" className="text-blue-600 hover:underline" target="_blank" rel="noopener noreferrer">Facebook: @SouthwestShortTermStays</a></p>
              </div>
              <div className="flex justify-center space-x-4 mb-6">
                <a href="https://facebook.com/SouthwestShortTermStays" target="_blank" rel="noopener noreferrer" aria-label="Visit our Facebook page">
                  <svg className="w-6 h-6 text-blue-600 hover:text-blue-800" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M22 12c0-5.523-4.477-10-10-10S2 6.477 2 12c0 4.991 3.657 9.128 8.437 9.878v-6.987h-2.54V12h2.54V9.845c0-2.51 1.493-3.89 3.776-3.89 1.094 0 2.238.195 2.238.195v2.46h-1.26c-1.243 0-1.63.771-1.63 1.562V12h2.773l-.443 2.89h-2.33v6.988C18.343 21.128 22 16.991 22 12z" />
                  </svg>
                </a>
              </div>
              <div className="text-center">
                <button
                  onClick={toggleModal}
                  className="bg-yellow-400 text-blue-900 px-6 py-3 rounded-lg font-semibold hover:bg-yellow-500 transition-colors"
                  aria-label="Contact us for a free consultation"
                >
                  Get in Touch
                </button>
              </div>
            </div>
          </section>

          {/* Footer */}
          <footer className="bg-blue-900 text-white py-8">
            <div className="container mx-auto px-4">
              <div className="flex flex-col md:flex-row justify-between items-center">
                <p className="font-[Open Sans] mb-4 md:mb-0">
                  © 2025 Southwest Short Term Stays. All rights reserved.
                </p>
                <div className="flex space-x-4">
                  <a href="#" className="hover:text-yellow-400" aria-label="Privacy Policy">Privacy Policy</a>
                  <a href="#" className="hover:text-yellow-400" aria-label="Terms of Service">Terms of Service</a>
                </div>
              </div>
              <div className="mt-6">
                <iframe
                  src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3075.268689013372!2d-84.46694468461247!3d39.40034997949695!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x884051b7b7b7b7b7%3A0x7b7b7b7b7b7b7b7b!2sWest%20Chester%2C%20OH!5e0!3m2!1sen!2sus!4v1697051234567!5m2!1sen!2sus"
                  width="100%"
                  height="200"
                  style={{ border: 0 }}
                  allowFullScreen=""
                  loading="lazy"
                  referrerPolicy="no-referrer-when-downgrade"
                  title="Map of West Chester, OH"
                ></iframe>
              </div>
            </div>
          </footer>

          {/* Contact Modal */}
          {isModalOpen && (
            <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
              <div className="bg-white p-8 rounded-lg max-w-md w-full">
                <h2 className="text-2xl font-bold font-[Montserrat] mb-4">Contact Us</h2>
                {error && <p className="text-red-500 mb-4">{error}</p>}
                <div className="space-y-4">
                  <input
                    type="text"
                    name="name"
                    value={formData.name}
                    onChange={handleInputChange}
                    placeholder="Name"
                    className="w-full p-2 border rounded-lg"
                    aria-label="Name"
                    required
                  />
                  <input
                    type="email"
                    name="email"
                    value={formData.email}
                    onChange={handleInputChange}
                    placeholder="Email"
                    className="w-full p-2 border rounded-lg"
                    aria-label="Email"
                    required
                  />
                  <input
                    type="tel"
                    name="phone"
                    value={formData.phone}
                    onChange={handleInputChange}
                    placeholder="Phone"
                    className="w-full p-2 border rounded-lg"
                    aria-label="Phone"
                  />
                  <textarea
                    name="message"
                    value={formData.message}
                    onChange={handleInputChange}
                    placeholder="Message"
                    className="w-full p-2 border rounded-lg"
                    rows="4"
                    aria-label="Message"
                  ></textarea>
                  <div className="flex justify-end space-x-4">
                    <button
                      onClick={toggleModal}
                      className="bg-gray-300 text-gray-800 px-4 py-2 rounded-lg hover:bg-gray-400"
                      aria-label="Close contact modal"
                    >
                      Cancel
                    </button>
                    <button
                      onClick={handleSubmit}
                      className="bg-yellow-400 text-blue-900 px-4 py-2 rounded-lg hover:bg-yellow-500"
                      aria-label="Submit contact form"
                    >
                      Submit
                    </button>
                  </div>
                </div>
              </div>
            </
