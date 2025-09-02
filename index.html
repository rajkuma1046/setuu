import React, { useState, useEffect, useCallback, useRef, useMemo } from 'react';
import { initializeApp } from 'firebase/app';
import { 
    getAuth, 
    onAuthStateChanged, 
    GoogleAuthProvider, 
    signInWithPopup, 
    createUserWithEmailAndPassword, 
    signInWithEmailAndPassword, 
    signOut,
    signInAnonymously,
    signInWithCustomToken
} from 'firebase/auth';
import { 
    getFirestore, 
    doc, 
    setDoc, 
    getDoc, 
    collection, 
    getDocs,
    query,
    where,
    addDoc,
    Timestamp,
    runTransaction,
    setLogLevel
} from 'firebase/firestore';

// --- Firebase Configuration ---
const firebaseConfig = {
  apiKey: "AIzaSyDyqLW6K7aMZudaGHRvxrceQDaANQE4c4Q",
  authDomain: "local-to-firebass.firebaseapp.com",
  databaseURL: "https://local-to-firebass-default-rtdb.asia-southeast1.firebasedatabase.app",
  projectId: "local-to-firebass",
  storageBucket: "local-to-firebass.appspot.com",
  messagingSenderId: "121890064671",
  appId: "1:121890064671:web:9143764a66282571c1c82a"
};


// --- Helper Functions & Constants ---

const getDistanceFromLatLonInKm = (lat1, lon1, lat2, lon2) => {
    if (!lat1 || !lon1 || !lat2 || !lon2) return null;
    const R = 6371; // Radius of the earth in km
    const dLat = deg2rad(lat2 - lat1);
    const dLon = deg2rad(lon2 - lon1);
    const a =
        Math.sin(dLat / 2) * Math.sin(dLat / 2) +
        Math.cos(deg2rad(lat1)) * Math.cos(deg2rad(lat2)) *
        Math.sin(dLon / 2) * Math.sin(dLon / 2);
    const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
    return R * c; // Distance in km
};

const deg2rad = (deg) => deg * (Math.PI / 180);

// --- Icon Components ---

const Star = ({ filled, onClick, size = 24 }) => (
    <svg onClick={onClick} className={`cursor-pointer ${filled ? 'text-yellow-400' : 'text-gray-300'}`} fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg" width={size} height={size}><path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path></svg>
);
const ChefHatIcon = ({ className }) => <svg className={className} xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><path d="M12 3c1.93 0 3.5 1.57 3.5 3.5V12H8.5V6.5C8.5 4.57 10.07 3 12 3Z"/><path d="M8.5 12H4a2 2 0 0 0-2 2v2a2 2 0 0 0 2 2h16a2 2 0 0 0 2-2v-2a2 2 0 0 0-2-2h-4.5"/><path d="M8.5 12v8.5"/><path d="M15.5 12v8.5"/></svg>;
const MapPinIcon = () => <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"/><circle cx="12" cy="10" r="3"/></svg>;
const LogOutIcon = () => <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h4"/><polyline points="16 17 21 12 16 7"/><line x1="21" x2="9" y1="12" y2="12"/></svg>;
const HomeIcon = () => <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><path d="m3 9 9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/></svg>;
const DashboardIcon = () => <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><rect width="7" height="9" x="3" y="3" rx="1"/><rect width="7" height="5" x="14" y="3" rx="1"/><rect width="7" height="9" x="14" y="12" rx="1"/><rect width="7" height="5" x="3" y="16" rx="1"/></svg>;
const SearchIcon = () => <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.3-4.3"/></svg>;

// --- Reusable Components ---

const Spinner = () => <div className="animate-spin rounded-full h-8 w-8 border-b-2 border-white"></div>;
const FullPageSpinner = ({ message }) => (
    <div className="min-h-screen flex flex-col items-center justify-center bg-cream-100">
        <div className="animate-spin rounded-full h-16 w-16 border-b-4 border-amber-800"></div>
        <p className="text-amber-800 mt-4">{message}</p>
    </div>
);

// --- Page Components ---

const AuthComponent = ({ setPage, setUserData, auth, db, appId }) => {
    // ... (Component code remains the same as previous version)
    const [isLogin, setIsLogin] = useState(true);
    const [email, setEmail] = useState('');
    const [password, setPassword] = useState('');
    const [role, setRole] = useState('customer');
    const [error, setError] = useState('');
    const [loading, setLoading] = useState(false);

    const handleGoogleSignIn = async () => {
        setLoading(true);
        const provider = new GoogleAuthProvider();
        try {
            const result = await signInWithPopup(auth, provider);
            const user = result.user;
            const userDocRef = doc(db, `artifacts/${appId}/public/data/users`, user.uid);
            const userDoc = await getDoc(userDocRef);

            if (!userDoc.exists()) {
                 const chosenRole = window.prompt("To complete your registration, are you a 'customer' or a 'halvai'?", "customer");
                 if (chosenRole === 'halvai' || chosenRole === 'customer') {
                     const newUser = {
                         uid: user.uid, email: user.email, displayName: user.displayName, photoURL: user.photoURL,
                         role: chosenRole, isProfileComplete: chosenRole === 'customer'
                     };
                     await setDoc(userDocRef, newUser);
                     setUserData(newUser);
                 } else {
                    setError("You must select a valid role to continue.");
                    await signOut(auth);
                    setLoading(false);
                    return;
                 }
            } else {
                setUserData(userDoc.data());
            }
            setPage({ name: 'home' });
        } catch (error) {
            console.error("Google Sign-In Error:", error);
            setError(error.message);
        } finally {
            setLoading(false);
        }
    };
    
    const handleEmailPassword = async (e) => {
        e.preventDefault();
        setLoading(true);
        setError('');
        try {
            if (isLogin) {
                await signInWithEmailAndPassword(auth, email, password);
                setPage({ name: 'home' });
            } else {
                const result = await createUserWithEmailAndPassword(auth, email, password);
                const user = result.user;
                const newUser = {
                    uid: user.uid, email: user.email, displayName: email.split('@')[0], photoURL: '',
                    role: role, isProfileComplete: role === 'customer'
                };
                await setDoc(doc(db, `artifacts/${appId}/public/data/users`, user.uid), newUser);
                setUserData(newUser);
                setPage({ name: 'home' });
            }
        } catch (error) {
            console.error("Email/Password Auth Error:", error);
            setError(error.message);
        } finally {
            setLoading(false);
        }
    };

    return (
        <div className="min-h-screen flex items-center justify-center bg-cream-100 p-4">
            <div className="max-w-md w-full bg-white rounded-xl shadow-lg p-8 space-y-6 border border-gray-200">
                <div className="text-center">
                    <ChefHatIcon className="mx-auto h-12 w-12 text-amber-800" />
                    <h2 className="mt-4 text-3xl font-bold text-amber-900">{isLogin ? 'Welcome Back!' : 'Join Halvai Finder'}</h2>
                    <p className="mt-2 text-sm text-gray-600">Find the perfect confectioner for your special event.</p>
                </div>
                {error && <p className="text-red-500 text-sm text-center bg-red-100 p-2 rounded-md">{error}</p>}
                
                <form onSubmit={handleEmailPassword} className="space-y-6">
                    <input type="email" value={email} onChange={e => setEmail(e.target.value)} placeholder="Email address" required className="w-full input" />
                    <input type="password" value={password} onChange={e => setPassword(e.target.value)} placeholder="Password" required className="w-full input" />
                    {!isLogin && (
                         <div className="flex items-center justify-center space-x-4">
                            <label className="flex items-center space-x-2 cursor-pointer"><input type="radio" name="role" value="customer" checked={role === 'customer'} onChange={() => setRole('customer')} className="form-radio text-amber-600"/><span className="text-gray-700">I'm a Customer</span></label>
                            <label className="flex items-center space-x-2 cursor-pointer"><input type="radio" name="role" value="halvai" checked={role === 'halvai'} onChange={() => setRole('halvai')} className="form-radio text-amber-600"/><span className="text-gray-700">I'm a Halvai</span></label>
                        </div>
                    )}
                    <button type="submit" disabled={loading} className="w-full btn-primary h-10 flex items-center justify-center">{loading ? <Spinner /> : (isLogin ? 'Log In' : 'Sign Up')}</button>
                </form>

                <div className="relative"><div className="absolute inset-0 flex items-center"><div className="w-full border-t border-gray-300"></div></div><div className="relative flex justify-center text-sm"><span className="px-2 bg-white text-gray-500">Or</span></div></div>

                <button onClick={handleGoogleSignIn} disabled={loading} className="w-full flex justify-center items-center space-x-2 bg-white border border-gray-300 text-gray-700 font-semibold py-2 px-4 rounded-md hover:bg-gray-50 transition duration-300">
                    <svg className="w-5 h-5" viewBox="0 0 48 48"><path fill="#4285F4" d="M24 9.5c3.54 0 6.71 1.22 9.21 3.6l6.85-6.85C35.9 2.38 30.47 0 24 0 14.62 0 6.51 5.38 2.56 13.22l7.98 6.19C12.43 13.72 17.74 9.5 24 9.5z"></path><path fill="#34A853" d="M46.98 24.55c0-1.57-.15-3.09-.38-4.55H24v9.02h12.94c-.58 2.96-2.26 5.48-4.78 7.18l7.73 6c4.51-4.18 7.09-10.36 7.09-17.65z"></path><path fill="#FBBC05" d="M10.53 28.59c-.48-1.45-.76-2.99-.76-4.59s.27-3.14.76-4.59l-7.98-6.19C.92 16.46 0 20.12 0 24c0 3.88.92 7.54 2.56 10.78l7.97-6.19z"></path><path fill="#EA4335" d="M24 48c6.48 0 11.87-2.13 15.84-5.73l-7.73-6c-2.52 1.7-5.74 2.68-9.11 2.68-6.26 0-11.57-4.22-13.47-9.91l-7.98 6.19C6.51 42.62 14.62 48 24 48z"></path><path fill="none" d="M0 0h48v48H0z"></path></svg>
                    <span>Continue with Google</span>
                </button>

                <p className="text-sm text-center text-gray-600">{isLogin ? "Don't have an account?" : "Already have an account?"}<button onClick={() => setIsLogin(!isLogin)} className="font-medium text-amber-700 hover:text-amber-600 ml-1">{isLogin ? 'Sign Up' : 'Log In'}</button></p>
            </div>
        </div>
    );
};

const HalvaiProfileSetup = ({ user, userData, setPage, setUserData, db, appId }) => {
    // ... (Component code remains the same as previous version)
    const [profile, setProfile] = useState({ halvaiName: '', specialty: '', description: '', bookingCostPerHour: '', contactNumber: '', address: '' });
    const [location, setLocation] = useState(null);
    const [loading, setLoading] = useState(false);
    const [error, setError] = useState('');

    const getLocation = () => {
        setLoading(true); setError('');
        if (navigator.geolocation) {
            navigator.geolocation.getCurrentPosition(position => {
                setLocation({ lat: position.coords.latitude, lng: position.coords.longitude });
                setLoading(false);
            }, () => { setError('Location access denied. Please enable it in your browser settings.'); setLoading(false); });
        } else { setError('Geolocation is not supported by your browser.'); setLoading(false); }
    };
    
    const handleSubmit = async (e) => {
        e.preventDefault();
        if (!location) { setError('Please set your location to be discoverable.'); return; }
        setLoading(true); setError('');
        try {
            await setDoc(doc(db, `artifacts/${appId}/public/data/halvaiProfiles`, user.uid), {
                ...profile, bookingCostPerHour: parseFloat(profile.bookingCostPerHour) || 0,
                location, averageRating: 0, ratingCount: 0, halvaiId: user.uid, email: user.email,
            });
            await setDoc(doc(db, `artifacts/${appId}/public/data/users`, user.uid), { isProfileComplete: true }, { merge: true });
            setUserData(prev => ({...prev, isProfileComplete: true}));
            setPage({ name: 'dashboard' });
        } catch (error) {
            console.error("Profile setup error:", error); setError(error.message);
        } finally { setLoading(false); }
    };
    
    return (
        <div className="min-h-screen bg-cream-100 p-4 sm:p-6 lg:p-8">
            <div className="max-w-2xl mx-auto bg-white rounded-xl shadow-lg p-8">
                <h2 className="text-3xl font-bold text-amber-900 mb-2">Setup Your Halvai Profile</h2>
                <p className="text-gray-600 mb-6">This information will be visible to customers in your area.</p>
                {error && <p className="text-red-500 text-sm mb-4">{error}</p>}
                <form onSubmit={handleSubmit} className="space-y-4">
                    <input name="halvaiName" value={profile.halvaiName} onChange={e => setProfile({...profile, halvaiName: e.target.value})} placeholder="Business Name (e.g., Gupta Sweets)" required className="w-full input" />
                    <input name="specialty" value={profile.specialty} onChange={e => setProfile({...profile, specialty: e.target.value})} placeholder="Specialty (e.g., Gajar Halwa, Soan Papdi)" required className="w-full input" />
                    <textarea name="description" value={profile.description} onChange={e => setProfile({...profile, description: e.target.value})} placeholder="Short description about your services" required className="w-full input h-24"></textarea>
                    <input name="bookingCostPerHour" type="number" value={profile.bookingCostPerHour} onChange={e => setProfile({...profile, bookingCostPerHour: e.target.value})} placeholder="Booking Cost (per hour, in ₹)" required className="w-full input" />
                    <input name="contactNumber" value={profile.contactNumber} onChange={e => setProfile({...profile, contactNumber: e.target.value})} placeholder="Contact Number" required className="w-full input" />
                    <input name="address" value={profile.address} onChange={e => setProfile({...profile, address: e.target.value})} placeholder="Full Address" required className="w-full input" />
                    
                    <div className="flex items-center space-x-4 p-3 bg-gray-50 rounded-lg border">
                        <MapPinIcon />
                        <div className="flex-grow">
                             {location ? <p className="text-sm text-green-700 font-medium">Location Set Successfully!</p> : <p className="text-sm text-gray-500">Your location is needed for customers to find you.</p>}
                        </div>
                        <button type="button" onClick={getLocation} className="btn-secondary whitespace-nowrap">{loading ? 'Getting...' : 'Set My Location'}</button>
                    </div>
                    <button type="submit" disabled={loading} className="w-full btn-primary h-10 flex justify-center items-center">{loading ? <Spinner/> : 'Save Profile'}</button>
                </form>
            </div>
        </div>
    );
};

const HomePage = ({ setPage, db, appId }) => {
    // ... (Component code remains the same as previous version)
    const [halvais, setHalvais] = useState([]);
    const [loading, setLoading] = useState(true);
    const [userLocation, setUserLocation] = useState(null);
    const [locationError, setLocationError] = useState('');
    const [searchTerm, setSearchTerm] = useState('');

    useEffect(() => {
        const fetchHalvais = async () => {
            if (!db || !appId) return;
            try {
                const querySnapshot = await getDocs(collection(db, `artifacts/${appId}/public/data/halvaiProfiles`));
                const halvaiList = querySnapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                setHalvais(halvaiList);
            } catch (err) {
                console.error("Error fetching halvais:", err);
                setLocationError("Could not fetch Halvai list. Please try again later.");
            } finally {
                setLoading(false);
            }
        };
        fetchHalvais();
    }, [db, appId]);

    const filteredHalvais = useMemo(() => {
        let sortedHalvais = [...halvais];
        if (userLocation) {
            sortedHalvais.forEach(h => {
                if (h.location) {
                    h.distance = getDistanceFromLatLonInKm(userLocation.lat, userLocation.lng, h.location.lat, h.location.lng);
                }
            });
            sortedHalvais.sort((a, b) => (a.distance ?? Infinity) - (b.distance ?? Infinity));
        }
        return sortedHalvais.filter(h => 
            h.halvaiName?.toLowerCase().includes(searchTerm.toLowerCase()) ||
            h.specialty?.toLowerCase().includes(searchTerm.toLowerCase())
        );
    }, [halvais, userLocation, searchTerm]);

    const findNearMe = () => {
        setLocationError('');
        setLoading(true);
        if (navigator.geolocation) {
            navigator.geolocation.getCurrentPosition(position => {
                setUserLocation({ lat: position.coords.latitude, lng: position.coords.longitude });
                setLoading(false);
            }, () => { setLocationError('Location access denied.'); setLoading(false); });
        } else { setLocationError('Geolocation is not supported.'); setLoading(false); }
    };
    
    return (
        <div className="bg-cream-100 min-h-screen">
            <header className="bg-white shadow-sm p-4 sticky top-0 z-10">
                <div className="container mx-auto">
                    <h1 className="text-3xl font-bold text-amber-900 text-center">Find Your Halvai</h1>
                    <p className="text-center text-gray-600 mt-1">Discover the best confectioners for any occasion in India</p>
                    <div className="mt-4 max-w-2xl mx-auto flex flex-col sm:flex-row gap-2">
                        <div className="relative flex-grow"><span className="absolute inset-y-0 left-0 flex items-center pl-3 text-gray-400"><SearchIcon /></span><input type="text" placeholder="Search by name or specialty..." value={searchTerm} onChange={e => setSearchTerm(e.target.value)} className="w-full input pl-10"/></div>
                        <button onClick={findNearMe} className="btn-primary flex items-center justify-center gap-2"><MapPinIcon /> Find Near Me</button>
                    </div>
                    {locationError && <p className="text-red-500 text-sm text-center mt-2">{locationError}</p>}
                </div>
            </header>
            <main className="container mx-auto p-4 sm:p-6 lg:p-8">
                {loading ? <div className="flex justify-center mt-10"><FullPageSpinner message="Fetching Halvais..." /></div> : (
                    <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                        {filteredHalvais.length > 0 ? filteredHalvais.map(halvai => (
                            <div key={halvai.id} className="bg-white rounded-xl shadow-md overflow-hidden transform hover:-translate-y-1 transition-transform duration-300">
                                <div className="p-6">
                                    <div className="flex justify-between items-start">
                                        <div>
                                            <p className="text-xs uppercase tracking-wide font-semibold text-amber-700">{halvai.specialty}</p>
                                            <h3 className="block mt-1 text-xl leading-tight font-bold text-black">{halvai.halvaiName}</h3>
                                        </div>
                                        <div className="flex items-center"><Star filled={true} size={20} /><span className="ml-1 text-gray-700 font-semibold">{(halvai.averageRating || 0).toFixed(1)}</span><span className="ml-1 text-gray-500 text-sm">({halvai.ratingCount || 0})</span></div>
                                    </div>
                                    <p className="mt-2 text-gray-500 truncate">{halvai.description}</p>
                                    <div className="mt-4 flex justify-between items-center">
                                        <div>
                                            <p className="text-lg font-semibold text-amber-900">₹{halvai.bookingCostPerHour}<span className="text-sm font-normal text-gray-600">/hr</span></p>
                                             {halvai.distance != null && <p className="text-sm text-gray-600 flex items-center mt-1"><MapPinIcon /> <span className="ml-1">{halvai.distance.toFixed(1)} km away</span></p>}
                                        </div>
                                        <button onClick={() => setPage({ name: 'halvaiProfile', props: { halvaiId: halvai.halvaiId } })} className="btn-secondary">View Profile</button>
                                    </div>
                                </div>
                            </div>
                        )) : (
                            <p className="text-center text-gray-500 col-span-full">No Halvais found. Try a different search or expand your area.</p>
                        )}
                    </div>
                )}
            </main>
        </div>
    );
};

const HalvaiProfilePage = ({ setPage, user, db, appId, halvaiId }) => {
    const [profile, setProfile] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState('');
    const [bookingDate, setBookingDate] = useState('');

    useEffect(() => {
        const fetchProfile = async () => {
            try {
                const docRef = doc(db, `artifacts/${appId}/public/data/halvaiProfiles`, halvaiId);
                const docSnap = await getDoc(docRef);
                if (docSnap.exists()) {
                    setProfile(docSnap.data());
                } else {
                    setError("Halvai profile not found.");
                }
            } catch (err) {
                setError("Failed to load profile.");
                console.error(err);
            } finally {
                setLoading(false);
            }
        };
        fetchProfile();
    }, [db, appId, halvaiId]);

    const handleBooking = async () => {
        if (!user) {
            alert("Please log in to book a Halvai.");
            setPage({ name: 'auth' });
            return;
        }
        if (!bookingDate) {
            alert("Please select a date for the booking.");
            return;
        }
        
        const bookingData = {
            halvaiId,
            customerId: user.uid,
            bookingDate: Timestamp.fromDate(new Date(bookingDate)),
            status: 'pending',
            createdAt: Timestamp.now(),
            customerEmail: user.email,
            halvaiName: profile.halvaiName
        };

        try {
            await addDoc(collection(db, `artifacts/${appId}/public/data/bookings`), bookingData);
            alert(`Booking request sent to ${profile.halvaiName} for ${new Date(bookingDate).toLocaleDateString()}!`);
        } catch (err) {
            alert("Failed to create booking. Please try again.");
            console.error(err);
        }
    };


    if (loading) return <FullPageSpinner message="Loading Profile..." />;
    if (error) return <div className="text-red-500 text-center p-8">{error}</div>;
    if (!profile) return null;

    return (
        <div className="bg-cream-100 min-h-screen p-4 sm:p-8">
            <div className="max-w-4xl mx-auto bg-white rounded-xl shadow-lg overflow-hidden">
                <div className="p-8">
                    <h2 className="text-4xl font-bold text-amber-900">{profile.halvaiName}</h2>
                    <p className="text-amber-700 font-semibold mt-1">{profile.specialty}</p>
                    <div className="flex items-center mt-2">
                        <Star filled={true} size={20} />
                        <span className="ml-2 text-gray-700 font-bold">{profile.averageRating.toFixed(1)}</span>
                        <span className="ml-1 text-gray-500">({profile.ratingCount} ratings)</span>
                    </div>
                    <p className="text-gray-600 mt-4">{profile.description}</p>
                    <div className="mt-6 grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div className="bg-gray-50 p-4 rounded-lg">
                            <h3 className="font-bold text-lg text-amber-800">Details</h3>
                            <p className="mt-2"><strong>Cost:</strong> ₹{profile.bookingCostPerHour}/hour</p>
                            <p><strong>Contact:</strong> {profile.contactNumber}</p>
                            <p><strong>Address:</strong> {profile.address}</p>
                        </div>
                         <div className="bg-gray-50 p-4 rounded-lg">
                             <h3 className="font-bold text-lg text-amber-800">Book Now</h3>
                             <p className="text-sm text-gray-500 mb-2">Select a date for your event.</p>
                             <input type="date" value={bookingDate} onChange={e => setBookingDate(e.target.value)} className="w-full input mb-2"/>
                             <button onClick={handleBooking} className="w-full btn-primary">Request Booking</button>
                         </div>
                    </div>
                </div>
            </div>
        </div>
    );
};

const DashboardPage = ({ user, userData, db, appId, setPage }) => {
    const [bookings, setBookings] = useState([]);
    const [loading, setLoading] = useState(true);

    useEffect(() => {
        if (!user || !userData) return;

        const fetchBookings = async () => {
            setLoading(true);
            const bookingsCol = collection(db, `artifacts/${appId}/public/data/bookings`);
            const q = userData.role === 'halvai'
                ? query(bookingsCol, where("halvaiId", "==", user.uid))
                : query(bookingsCol, where("customerId", "==", user.uid));
            
            try {
                const querySnapshot = await getDocs(q);
                const bookingsData = querySnapshot.docs.map(doc => ({id: doc.id, ...doc.data()}));
                setBookings(bookingsData);
            } catch (err) {
                console.error("Failed to fetch bookings:", err);
            } finally {
                setLoading(false);
            }
        };

        fetchBookings();
    }, [user, userData, db, appId]);


    return (
        <div className="container mx-auto p-8">
            <h1 className="text-3xl font-bold text-amber-900">Dashboard</h1>
            <p className="text-gray-600">Welcome, {user.displayName || user.email}!</p>

            <div className="mt-8 bg-white p-6 rounded-xl shadow-lg">
                <h2 className="text-xl font-bold text-amber-800 mb-4">{userData.role === 'halvai' ? "Your Booking Requests" : "Your Bookings"}</h2>
                 {loading ? <Spinner /> : (
                     bookings.length > 0 ? (
                        <ul className="space-y-3">
                            {bookings.map(b => (
                                <li key={b.id} className="p-4 bg-gray-50 rounded-lg flex justify-between items-center">
                                    <div>
                                        <p className="font-semibold">{userData.role === 'halvai' ? `From: ${b.customerEmail}` : `With: ${b.halvaiName}`}</p>
                                        <p className="text-sm text-gray-500">Date: {b.bookingDate.toDate().toLocaleDateString()}</p>
                                    </div>
                                    <span className={`px-3 py-1 text-sm font-semibold rounded-full ${b.status === 'pending' ? 'bg-yellow-200 text-yellow-800' : 'bg-green-200 text-green-800'}`}>
                                        {b.status}
                                    </span>
                                </li>
                            ))}
                        </ul>
                     ) : (
                        <p className="text-gray-500">No bookings found.</p>
                     )
                 )}
            </div>
        </div>
    );
};


// --- Main App Component ---
export default function App() {
    const [page, setPage] = useState({ name: 'home', props: {} });
    const [user, setUser] = useState(null);
    const [userData, setUserData] = useState(null);
    const [auth, setAuth] = useState(null);
    const [db, setDb] = useState(null);
    const [appId, setAppId] = useState(null);
    const [isAuthReady, setIsAuthReady] = useState(false);
    
    const isFirebaseInitialized = useRef(false);

    useEffect(() => {
        if (isFirebaseInitialized.current) return;
        isFirebaseInitialized.current = true;

        try {
            const finalFirebaseConfig = typeof __firebase_config !== 'undefined' && __firebase_config
                ? JSON.parse(__firebase_config)
                : firebaseConfig;
            const currentAppId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
            
            const firebaseApp = initializeApp(finalFirebaseConfig);
            const firebaseAuth = getAuth(firebaseApp);
            const firestoreDb = getFirestore(firebaseApp);
            setLogLevel('debug');

            setAuth(firebaseAuth);
            setDb(firestoreDb);
            setAppId(currentAppId);

            const unsubscribe = onAuthStateChanged(firebaseAuth, async (currentUser) => {
                if (currentUser) {
                    setUser(currentUser);
                    const userDocRef = doc(firestoreDb, `artifacts/${currentAppId}/public/data/users`, currentUser.uid);
                    const userDoc = await getDoc(userDocRef);
                    if (userDoc.exists()) {
                        setUserData(userDoc.data());
                    }
                } else {
                    setUser(null);
                    setUserData(null);
                }
                setIsAuthReady(true);
            });

            (async () => {
                try {
                    if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                        await signInWithCustomToken(firebaseAuth, __initial_auth_token);
                    } else {
                        await signInAnonymously(firebaseAuth);
                    }
                } catch (error) {
                     console.error("Initial sign-in failed:", error);
                }
            })();

            return () => unsubscribe();
        } catch (e) {
            console.error("Firebase initialization failed:", e);
            setIsAuthReady(true);
        }
    }, []);

    const renderPage = () => {
        if (!isAuthReady || !db) {
            return <FullPageSpinner message="Connecting to service..." />;
        }
        
        const pageProps = { ...page.props, setPage, user, userData, setUserData, auth, db, appId };

        if (user && userData?.role === 'halvai' && !userData.isProfileComplete && page.name !== 'profileSetup') {
            return <HalvaiProfileSetup {...pageProps} />;
        }
        
        switch (page.name) {
            case 'auth': return <AuthComponent {...pageProps} />;
            case 'profileSetup': return user ? <HalvaiProfileSetup {...pageProps} /> : <AuthComponent {...pageProps} />;
            case 'halvaiProfile': return <HalvaiProfilePage {...pageProps} />;
            case 'dashboard': return user && userData ? <DashboardPage {...pageProps} /> : <AuthComponent {...pageProps} />;
            default: return <HomePage {...pageProps} />;
        }
    };
    
    return (
        <div className="font-sans antialiased bg-cream-100">
            <style>{`:root { --cream-100: #FFF8F0; --amber-700: #B45309; --amber-800: #92400E; --amber-900: #78350F; } .input { @apply w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-amber-500 transition; } .btn-primary { @apply bg-amber-800 text-white font-bold py-2 px-4 rounded-md hover:bg-amber-900 transition duration-300 disabled:bg-gray-400; } .btn-secondary { @apply bg-amber-100 border border-amber-700 text-amber-800 font-bold py-2 px-4 rounded-md hover:bg-amber-200 transition duration-300; } .nav-link { @apply flex items-center space-x-2 text-gray-600 hover:text-amber-800 font-semibold transition; }`}</style>
            {isAuthReady && auth && <nav className="bg-white shadow-md py-3 px-6 sticky top-0 z-20">
                <div className="container mx-auto flex justify-between items-center">
                    <div className="flex items-center space-x-2 cursor-pointer" onClick={() => setPage({ name: 'home' })}><ChefHatIcon className="text-amber-800 h-7 w-7" /><span className="text-xl font-bold text-amber-900">Halvai Finder</span></div>
                    <div className="flex items-center space-x-4">
                         <button onClick={() => setPage({ name: 'home' })} className="nav-link"><HomeIcon /> <span className="hidden sm:inline">Home</span></button>
                        {user ? (
                            <>
                                {userData && <button onClick={() => setPage({ name: 'dashboard' })} className="nav-link"><DashboardIcon /> <span className="hidden sm:inline">Dashboard</span></button>}
                                <button onClick={() => {signOut(auth); setPage({name:'home'})}} className="nav-link text-red-600"><LogOutIcon /> <span className="hidden sm:inline">Logout</span></button>
                            </>
                        ) : (
                            <button onClick={() => setPage({ name: 'auth' })} className="btn-primary">Login / Sign Up</button>
                        )}
                    </div>
                </div>
            </nav>}
            {renderPage()}
        </div>
    );
}

