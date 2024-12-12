# Expert-Survey
import React, { useState } from 'react';
import { Input } from '@/components/ui/input';
import { Textarea } from '@/components/ui/textarea';
import { Button } from '@/components/ui/button';
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card';
import { Check } from 'lucide-react';

const IndianTransportTechnologySurvey = () => {
  const [formData, setFormData] = useState({
    name: '',
    profession: '',
    region: '',
    topTechnologies: ['', '', ''],
    socialInclusivityImpact: '',
    economicEmpowermentPotential: '',
    accessibilityImprovements: '',
    implementationChallenges: '',
    additionalInsights: ''
  });

  const [submitted, setSubmitted] = useState(false);

  const indianTransportTechnologies = [
    {
      category: 'Digital Payment & Ticketing',
      technologies: [
        'UPI-based Transport Payments',
        'Mobile Ticketing Systems',
        'Unified Multimodal Ticketing',
        'Automatic Ticket Vending Machines',
        'QR Code-based Ticketing'
      ]
    },
    {
      category: 'Mobility Solutions',
      technologies: [
        'Ridesharing Platforms',
        'Community Transportation Apps',
        'Ride-hauling Services',
        'Affordable Electric Vehicle Sharing',
        'Last-mile Connectivity Solutions'
      ]
    },
    {
      category: 'Accessibility Technologies',
      technologies: [
        'Low-cost GPS Tracking for Public Transport',
        'Real-time Accessibility Information',
        'Multilingual Transport Navigation Apps',
        'Inclusive Design Transportation Interfaces',
        'Affordable Smartphone-based Transport Solutions'
      ]
    }
  ];

  const handleChange = (e, field, index = null) => {
    const value = e.target.value;
    if (index !== null) {
      const newTopTechnologies = [...formData.topTechnologies];
      newTopTechnologies[index] = value;
      setFormData(prev => ({
        ...prev,
        topTechnologies: newTopTechnologies
      }));
    } else {
      setFormData(prev => ({
        ...prev,
        [field]: value
      }));
    }
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    // In a real application, you'd send this data to a backend
    console.log(formData);
    setSubmitted(true);
  };

  if (submitted) {
    return (
      <Card className="w-full max-w-2xl mx-auto mt-8 bg-green-50">
        <CardHeader>
          <CardTitle className="flex items-center text-green-600">
            <Check className="mr-2" /> Survey Submitted Successfully
          </CardTitle>
        </CardHeader>
        <CardContent>
          <p>धन्यवाद! (Thank you!) Your insights will help shape more inclusive transportation technologies in India.</p>
          <p className="mt-4 text-sm text-gray-600">
            Your responses contribute to understanding technology's role in social equity and transportation.
          </p>
        </CardContent>
      </Card>
    );
  }

  return (
    <div className="w-full max-w-3xl mx-auto p-4">
      <Card>
        <CardHeader>
          <CardTitle className="text-2xl">
            भारतीय परिवहन प्रौद्योगिकी सर्वेक्षण
            <br />
            <span className="text-sm text-gray-600">
              (Indian Transportation Technology Survey)
            </span>
          </CardTitle>
          <p className="text-sm text-gray-600">
            समावेशी और न्यायसंगत परिवहन प्रणालियों में प्रौद्योगिकी के प्रभाव को समझना
            (Understanding Technology's Impact on Inclusive Transportation Systems)
          </p>
        </CardHeader>
        <CardContent>
          <form onSubmit={handleSubmit} className="space-y-6">
            {/* Personal Information */}
            <div className="grid grid-cols-2 gap-4">
              <div>
                <label className="block mb-2">Name / नाम</label>
                <Input 
                  value={formData.name}
                  onChange={(e) => handleChange(e, 'name')}
                  placeholder="Enter your name"
                  required
                />
              </div>
              <div>
                <label className="block mb-2">Profession / पेशा</label>
                <Input 
                  value={formData.profession}
                  onChange={(e) => handleChange(e, 'profession')}
                  placeholder="Your professional background"
                  required
                />
              </div>
              <div className="col-span-2">
                <label className="block mb-2">Region / क्षेत्र</label>
                <Input 
                  value={formData.region}
                  onChange={(e) => handleChange(e, 'region')}
                  placeholder="Your state/city/region"
                  required
                />
              </div>
            </div>

            {/* Technology Selection */}
            <div className="space-y-4">
              <h3 className="text-lg font-semibold">
                Select Top 3 Transportation Technologies / 
                शीर्ष 3 परिवहन प्रौद्योगिकियाँ चुनें
              </h3>
              {indianTransportTechnologies.map((category) => (
                <div key={category.category} className="border-b pb-4">
                  <h4 className="font-medium mb-2">{category.category}</h4>
                  <div className="grid grid-cols-3 gap-2">
                    {category.technologies.map((tech) => (
                      <label key={tech} className="flex items-center space-x-2 cursor-pointer">
                        <input
                          type="checkbox"
                          value={tech}
                          checked={formData.topTechnologies.includes(tech)}
                          onChange={() => {
                            const currentTechs = formData.topTechnologies;
                            const techIndex = currentTechs.indexOf(tech);
                            let newTechs;

                            if (techIndex > -1) {
                              newTechs = currentTechs.filter(t => t !== tech);
                            } else if (currentTechs.filter(t => t).length < 3) {
                              newTechs = [...currentTechs.filter(t => t), tech];
                            } else {
                              return;
                            }

                            while (newTechs.length < 3) {
                              newTechs.push('');
                            }

                            setFormData(prev => ({
                              ...prev,
                              topTechnologies: newTechs
                            }));
                          }}
                          className="form-checkbox"
                        />
                        <span>{tech}</span>
                      </label>
                    ))}
                  </div>
                </div>
              ))}
            </div>

            {/* Detailed Impact Questions */}
            <div className="space-y-4">
              <div>
                <label className="block mb-2">
                  How will these technologies improve social inclusivity? / 
                  ये प्रौद्योगिकियाँ सामाजिक समावेशिता में कैसे सुधार करेंगी?
                </label>
                <Textarea
                  value={formData.socialInclusivityImpact}
                  onChange={(e) => handleChange(e, 'socialInclusivityImpact')}
                  placeholder="Describe potential social inclusion impacts"
                  rows={3}
                />
              </div>
              <div>
                <label className="block mb-2">
                  Potential for economic empowerment / 
                  आर्थिक सशक्तिकरण की क्षमता
                </label>
                <Textarea
                  value={formData.economicEmpowermentPotential}
                  onChange={(e) => handleChange(e, 'economicEmpowermentPotential')}
                  placeholder="Discuss economic opportunities created"
                  rows={3}
                />
              </div>
              <div>
                <label className="block mb-2">
                  Improvements in accessibility / 
                  पहुँच में सुधार
                </label>
                <Textarea
                  value={formData.accessibilityImprovements}
                  onChange={(e) => handleChange(e, 'accessibilityImprovements')}
                  placeholder="How technology can make transportation more accessible"
                  rows={3}
                />
              </div>
              <div>
                <label className="block mb-2">
                  Implementation challenges / 
                  कार्यान्वयन की चुनौतियाँ
                </label>
                <Textarea
                  value={formData.implementationChallenges}
                  onChange={(e) => handleChange(e, 'implementationChallenges')}
                  placeholder="Discuss potential barriers to technology adoption"
                  rows={3}
                />
              </div>
              <div>
                <label className="block mb-2">
                  Additional insights / 
                  अतिरिक्त अंतर्दृष्टि
                </label>
                <Textarea
                  value={formData.additionalInsights}
                  onChange={(e) => handleChange(e, 'additionalInsights')}
                  placeholder="Share any other thoughts or ideas"
                  rows={3}
                />
              </div>
            </div>

            {/* Submission */}
            <div className="flex justify-between items-center">
              <label className="flex items-center space-x-2">
                <input type="checkbox" required className="form-checkbox" />
                <span>
                  I consent to my anonymous responses being used for research /
                  मैं अपनी अनाम प्रतिक्रियाओं के शोध में उपयोग के लिए सहमति देता/देती हूँ
                </span>
              </label>
              <Button type="submit" className="bg-blue-600 hover:bg-blue-700">
                Submit Survey / सर्वेक्षण जमा करें
              </Button>
            </div>
          </form>
        </CardContent>
      </Card>
    </div>
  );
};

export default IndianTransportTechnologySurvey;
