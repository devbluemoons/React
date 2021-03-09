## State
  
## array state
```jsx
// bad
const list = someList;

// good
const list = [...someList];

// example
const [production, setProduction] = useState({});
const [jobList, setJobList] = useState([]);

useEffect(() => {
		if (production?.jobList) {
			  const list = [...production.jobList];
			  list.sort((a, b) => a.mesOrder - b.mesOrder);
			setJobList(list);
		}
}, [production.jobList]);
```
