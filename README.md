## useState Hook (Memory)
* `useState` React ki temporary memory hai.
* Jab variable badalta hai, to yeh screen ko automatic refresh (re-render) kar deta hai.

## Conditional Rendering (Limit Control)
* `if (count < 4)` lagane se hum state ko ek limit par freeze kar sakte hain.
* Yeh real-world mein OTP limits ya shopping cart max quantity selector mein use hota hai.
* ## 3. Arrow Function and Brackets Rule `{ }`

React mein button ke click event (`onClick`) par brackets kab lagane hain aur kab nahi, iska simple rule yeh hai:

### 1. Jab sirf EK state change karni ho (Single Line):
Agar sirf ek kaam karna ho to curly braces `{ }` ki zaroorat nahi hoti. Arrow `=>` ke baad direct code likh dete hain.
* **Example:** `onClick={() => setCounter(count + 1)}`

### 2. Jab EK SE ZYADA (Multiple) states change karni hon (Block of Code):
Jab 2 ya us se zyada states ko ek sath update karna ho, to arrow `=>` ke baad **curly braces `{ }`** lagana LAZMI hai. Is boundary ke andar har statement ke aakhir mein semicolon `;` bhi lagaya jata hai.
* **Example:**
  ```jsx
  onClick={() => {
      setCounter(5);     // Kaam #1
      setIncrease(10);   // Kaam #2
  }}
## 4. Toggle Concept & Real-World Uses
Toggle ka matlab hai ek hi state ko ON/OFF ya True/False mein switch karna.
* **Mobile Navbar:** Button click par menu ka show aur hide hona.
* **Dark Mode:** Light aur dark theme ke darmiyan switch karna.
* **FAQs Section:** Sawal par click karne se jawab ka open aur close hona.
* 📌 React Weather App — Key Logic & Notes

1. Controlled Inputs & Sanitization (.trim())
- Logic: Input field ko React State (city) ke sath bind karte hain taaki UI aur State hamesha sync rahein.
- Key Learning: if (!city.trim()) return;
  * .trim() spaces ko remove karta hai.
  * User ke khali ya space input par fuzool/unnecessary API calls ko rokta hai.

2. Event Execution & Asynchronous API Handling
- Logic: API call tabhi chalegi jab user button click karega (onClick={fetchWeather}).
- Key Flow:
  1. Reset State: Fetch start hote hi purana data clear karo (setWeatherData(null), setError("")) aur loader set karo (setLoading(true)).
  2. Fetch Data: await fetch(url) async request bhejta hai aur background me response ka wait karta hai.
  3. Cleanup: finally block hamesha chalta hai taaki loading spinner stop ho sake (setLoading(false)).

3. Error Handling (try...catch & throw)
- Logic: fetch() network failures ko to Catch me bhejta hai, lekin API ke errors (jaise 404 City Not Found ya 401 Invalid Key) par crash nahi hota.
- Key Learning: if (!response.ok) throw new Error(data.message)
  * Hum khud API status check karke manual error throw karte hain jo catch(err) me chala jata hai aur state update kar deta hai.

4. Conditional Rendering (&& Operator)
- Logic: JSX me UI elements ko state ki condition par hide/show karna.
- Examples:
  * {loading && <p>Loading...</p>} -> Jab tak data fetch ho raha hai.
  * {error && <p>{error}</p>} -> Jab koi error aaye.
  * {weatherData && <div>...</div>} -> Jab API se valid data mil jaye.

5. Optional Chaining (?.) Safety
- Logic: {weatherData.sys?.country} ya {weatherData.main?.temp}
- Key Learning: Nested JSON objects ko safe access karne ke liye ?. lagate hain. Agar API me wo property null ya undefined ho, to app crash nahi hoti.

6. Environment Variables (.env)
- Logic: Sensitive keys ko source code se alag rakhna.
- Vite Rule: File name strictly .env hona chahiye, variable name VITE_ se start hona chahiye (VITE_WEATHER_API_KEY), aur change karne ke baad Dev Server Restart karna zaroori hai.
* # React useState Concept

React mein `useState` tab use hota hai jab hum chahte hain ke variable ki value badalne par **screen bhi automatic update (render) ho**.

## Syntax:
```jsx
const [count, setCount] = useState(0);
