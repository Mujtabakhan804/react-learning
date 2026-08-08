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
Aap niche diye gaye box se poore notes asani se copy kar sakte hain:

```markdown
# 📌 JavaScript: `fetch` and `async/await` Notes

---

### 1. `fetch()` kya hai?
* **Definition:** `fetch()` JavaScript ka ek built-in web API function hai jo browser se server/API ko Network Requests (HTTP requests) bhejne ke liye use hota hai.
* **Return Value:** Yeh hamesha ek **Promise** return karta hai.
* **Basic Syntax:**
  ```javascript
  fetch(url)

### 2. `async / await` kya hai?

* **`async` Keyword:** Jab aap kisi function ke shuru mein `async` likhte hain, toh woh function asynchronous ban jata hai aur hamesha ek Promise return karta hai.
* **`await` Keyword:** Yeh sirf `async` function ke andar use hota hai. Yeh JavaScript ko kehta hai ke jab tak Promise resolve na ho jaye (yaani response na aa jaye), tab tak aage ki line par mat jao.
* **Fayda:** Code bilkul clean aur readable lagta hai (synchronous code ki tarah).

---

### 💡 Complete Example with Explanation

Yeh ek real-world weather API request ki example hai jisme Error Handling aur Try-Catch bhi shamil hai:

```javascript
// 1. Function ko 'async' banayein
const fetchWeatherData = async (cityName) => {
  
  // Try-Catch block taake network ya API errors handle ho sakein
  try {
    const apiKey = "YOUR_API_KEY";
    
    // 2. 'await' lagaya taake fetch ka response aane tak code ruke
    const response = await fetch(
      `[https://api.openweathermap.org/data/2.5/weather?q=$](https://api.openweathermap.org/data/2.5/weather?q=$){cityName}&appid=${apiKey}`
    );

    // 3. Status Check: Agar response OK nahi hai (e.g. 404 City Not Found)
    if (!response.ok) {
      throw new Error("City nahi mili ya API Key galat hai!");
    }

    // 4. Response ko JSON format mein convert karein ('await' ke sath)
    const data = await response.json();

    // Data ready hai!
    console.log("Weather Data:", data);
### 🛠️ Step-by-Step Flow (Samajhne ke liye)

1. **Request Send:** `fetch(url)` server ko request bhejta hai.
2. **Response Wait:** `await fetch()` jab tak network se response nahi milta, execution ko usi line par rok ke rakhta hai.
3. **HTTP Status Check:** `response.ok` check karta hai ke response status 200–299 ke darmayan hai ya nahi.
4. **JSON Conversion:** `response.json()` stream response ko readable JS Object mein convert karta hai (is mein bhi `await` lagta hai).
5. **Error Safety:** `try...catch` ensure karta hai ke agar API server down ho ya network gayab ho, toh app crash na ho balke catch block chal jaye.

---

### 🎯 Quick Recap / Golden Rules

* 🟢 **Rule 1:** Har asynchronous function ke aage `async` likhein.
* 🟢 **Rule 2:** `fetch()` aur `.json()` dono Promise return karte hain, isliye dono ke sath `await` lagayein.
* 🟢 **Rule 3:** API requests mein `try...catch` hamesha use karein taake errors ko easily catch kiya ja sake.

```
📌 React useEffect Key Notes

1. useEffect UI/JSX Return Nahi Kar Sakta

Purpose: Iska kaam sirf background tasks (API call, event listeners) handle karna hai.

Cleanup Reserved: Iska return sirf cleanup functions (memory/timer clear karne) ke liye use hota hai.

UI Handling: Loading/Error check aur JSX (<div>) hamesha component ki main body mein return hote hain.

2. fetchData() Ko Call Karne Ki Waja

Execution: Function sirf async () => {} define karne se nahi chalta, usko explicitly call karna padta hai.

React Rule: useEffect(async () => ...) React mein invalid syntax hai, is liye andar function banakar immediately call kiya jata hai.

3. Dependency Array [] Ka Role

Execution Control: Yeh tay karta hai ke effect kab aur kitni baar chalega.

Empty Array []: Code sirf 1 baar chalega (Component Load hone par).

Without Array: Har re-render par chalega, jis se Infinite Loop ban jayega.

With Variable [category]: Jab bhi wo variable/state change hoga, useEffect automatic dobara chalega.

    console.log("Temperature:", data.main.temp);

  } catch (error) {
    // Agar poore process mein koi bhi masla aaye (e.g. Internet breakdown)
    console.error("Error aaya hai:", error.message);
  }
};

// Function Call
fetchWeatherData("Lahore");



