# Bengali Shop with Dynamic Prices & Stripe Checkout

This single-file web application simulates a Bengali shop (আমার বাংলা দোকান) where item prices dynamically fluctuate every second. Users can browse items, add them to a shopping cart, adjust quantities, and proceed to a simulated checkout process using Stripe.

## How to Use

1.  **Open `index.html`**: Simply open the `index.html` file in your web browser. No special server setup is required.
2.  **Browse Items**: Observe the prices of items in the "দোকানের জিনিসপত্র (Shop Items)" section. These prices will change every second, providing real-time market simulation.
3.  **Add to Cart**: Click the "Add to Cart" button next to any item to add it to "আমার কেনাকাটা (My Cart)".
4.  **Manage Cart**: In the cart section, you can use the `+` and `-` buttons to adjust the quantity of items. Reducing an item's quantity to zero will remove it from the cart. The cart total automatically updates, reflecting the current dynamic prices of the items.
5.  **Checkout**: Click the "চেকআউট (Checkout)" button. This will attempt to redirect you to a Stripe checkout page.
    *   **Note**: For actual payment processing, a valid Stripe Publishable Key (`pk_live_...`) and a secure backend server to create Stripe Checkout Sessions are typically required. This demonstration uses a placeholder test key and client-side redirection, so it will only simulate the *initiation* of a Stripe checkout, not a completed transaction without further backend integration.
    *   **Stripe Publishable Key**: The application uses a placeholder test key (`pk_test_TYooMQauvdEDq54NiTgbOGBZ`). To test with your own Stripe account, you should replace this value in the `index.html` file with your actual publishable key.

## Code Explanation

This project is a single-file application (`index.html`) utilizing only HTML for structure, CSS for styling (inline in `<style>` tags), and vanilla JavaScript for all interactive functionalities.

*   **HTML Structure**:
    *   The page is divided into two main sections: a "Shop Items" list and a "Shopping Cart" display.
    *   Basic styling is applied directly within the `<style>` tag to achieve a clean and readable layout, with subtle Bengali cultural cues (e.g., using brown tones).
*   **Dynamic Pricing (JavaScript)**:
    *   An array `shopItems` holds the initial data for each product, including a `basePrice`.
    *   The `generateDynamicPrice` function introduces a random fluctuation (up to +/- 15%) around the `basePrice` to simulate market changes.
    *   The `updateAllPrices` function is called every second using `setInterval`, recalculating and updating the displayed price for each item. Visual feedback (green for price increases, red for decreases) is briefly shown to highlight changes.
*   **Shopping Cart (JavaScript)**:
    *   A global `cart` object (`{ itemId: { item, quantity } }`) stores the items selected by the user.
    *   `addToCart` and `updateCartItemQuantity` functions handle adding items, incrementing quantities, or removing items from the cart.
    *   The `renderCart` function is responsible for updating the cart's display in the DOM. Crucially, it fetches the *latest dynamic price* for each item from the `shopItems` array before calculating the total, ensuring the cart always reflects the most current market prices.
*   **Stripe Integration (JavaScript)**:
    *   The `Stripe.js` library (version 3) is included from its CDN.
    *   The `checkout` function collects all items currently in the `cart`, formats them into Stripe-compatible `lineItems` (converting prices to cents and specifying `bdt` for Bangladeshi Taka currency).
    *   It then uses `stripe.redirectToCheckout` to redirect the user to a Stripe-hosted checkout page. Placeholder URLs are provided for `successUrl` and `cancelUrl` as this is a client-side only demonstration.

## License

This project is licensed under the MIT License.