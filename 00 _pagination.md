## pagination
  
```js
import { useState, useEffect } from "react";

function Paging({ totalCount, currentPage, onCurrentPage, pageRow }) {
	// state
	const [pagination, setPagination] = useState({
		pageSize: pageRow,
		rangeSize: 10,
		totalPages: 0,
		rangeCount: 0,
	});
	const [pages, setPages] = useState([]);
	const [pageGroup, setPageGroup] = useState([]);

	// event
	const onPrev = page => {
		if (page < 1) {
			return;
		}
		onCurrentPage(page);
	};
	const onNext = page => {
		if (page > pagination.totalPages) {
			return;
		}
		onCurrentPage(page);
	};
	const onCurrent = page => onCurrentPage(page);

	// watch
	useEffect(() => {
		const totalPages = Math.ceil(totalCount / pageSize);
		const rangeCount = Math.ceil(totalPages / rangeSize);

		setPagination(prevState => ({
			...prevState,
			totalPages: totalPages,
			rangeCount: rangeCount,
		}));

		if (rangeCount) {
			const frame = Array.from(Array(rangeCount), () => []);

			for (let i = 1; i <= totalPages; i++) {
				frame[Math.ceil(i / rangeSize) - 1].push(i);
			}

			setPageGroup(frame);
		}
	}, [totalCount]);

	useEffect(() => {
		const currentPageGroup = pageGroup[Math.ceil(currentPage / rangeSize) - 1];
		setPages(currentPageGroup);
	}, [currentPage, pageGroup]);

	// variable
	const { pageSize, rangeSize } = pagination;

	// view
	return (
		<div className="paging-container">
			<div className="paging-box">
				<a href="#!" className="prev" onClick={() => onPrev(currentPage - 1)}></a>
				{pages?.map(page => (
					<a
						href="#!"
						key={page}
						className={page === currentPage ? "on" : ""}
						onClick={() => onCurrent(page)}
					>
						{page}
					</a>
				))}
				<a href="#!" className="next" onClick={() => onNext(currentPage + 1)}></a>
			</div>
		</div>
	);
}

export default Paging;

```
