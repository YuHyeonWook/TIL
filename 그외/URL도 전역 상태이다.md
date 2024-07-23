## URL도 전역 상태이다.

- 네이버 쇼핑몰 처럼 URL에 값을 저장해놓고 가져오고 있다. 이는 새로고침을 할 때, 다른 사용자에게 공유할 때 값을 유지한다는 특징이 있다. 그래서 URL은 어디서든 접근할 수 있으니 태생부터 전역변수이다.

![image](https://github.com/user-attachments/assets/ba71b536-c1fe-4afa-8e69-b1a6b137ed0f)

- URL은 path 말고 query에 담아야 한다. 왜냐하면, path는 웹 리소스의 위치를 나타내고, 정렬이나 필터링을 한다면 query Parameter를 사용한다.
- MDN에 URLSearchParams 생성자를 사용하면 손쉽게 쿼리 스트링을 다룰 수 있다. https://developer.mozilla.org/ko/docs/Web/API/URLSearchParams/URLSearchParams
- URL이라는 생성자를 사용하면 URL을 쉽게 파싱할 수 있다는 것, window.location.search를 사용하면 쿼리스트링을 쉽게 따올 수 있다.
- react-router-dom에도 useSearchParams 라는 훅이 있고, 이것의 리턴값도
  URLSearchParams에 기반하고 있다.

```tsx
function App() {
const [products, setProducts] = useState([]);
const [searchParams, setSearchParams] = useSearchParams();
const [isLoggedIn, setIsLoggedIn] = useState(false);
// 상태 -> 계산으로 변경
const category = searchParams.get('category') || '';
const maxPrice = searchParams.get('maxPrice') || '';
const color = searchParams.get('color') || '';
const size = searchParams.get('size') || '';
const rating = searchParams.get('rating') || '';
const inStock = searchParams.get('inStock') === 'true';

useEffect(() => {
fetchProducts().then(data => {
setProducts(data);
});
checkLoginStatus().then(status => {
setIsLoggedIn(status);
});
}, []);

useEffect(() => {
// 상태를 URLSearchParams 객체로 업데이트
const newSearchParams = new URLSearchParams();
if (category) newSearchParams.set('category', category);
if (maxPrice) newSearchParams.set('maxPrice', maxPrice);
if (color) newSearchParams.set('color', color);
if (size) newSearchParams.set('size', size);
if (rating) newSearchParams.set('rating', rating);
if (inStock) newSearchParams.set('inStock', inStock.toString());
setSearchParams(newSearchParams, { replace: true });
}, [category, maxPrice, color, size, rating, inStock]);

const filteredProducts = products.filter(product =>
(category ? product.category === category : true) &&
(maxPrice ? product.price <= maxPrice : true) &&
(color ? product.color === color : true) &&
(size ? product.size === size : true) &&
(rating ? product.rating >= rating : true) &&
(inStock ? product.inStock : true)
);

return (
<div>
<h1>Product List</h1>
<Filter
category={category}
maxPrice={maxPrice}
setCategory={value => setSearchParams({ ...searchParams, category: valu
setMaxPrice={value => setSearchParams({ ...searchParams, maxPrice: valu
/>
<Products products={filteredProducts} />
{isLoggedIn && (
<button onClick={() => {/* modal control logic */}}>Open Additional Fil
)}
{/* Modal component logic */}
</div>
);
}

export default App;
```
