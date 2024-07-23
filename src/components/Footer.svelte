<script>
	const year = new Date().getFullYear();

	const romanYear = (year) => {
		const roman = {
			M: 1000,
			CM: 900,
			D: 500,
			CD: 400,
			C: 100,
			XC: 90,
			L: 50,
			XL: 40,
			X: 10,
			IX: 9,
			V: 5,
			IV: 4,
			I: 1
		};
		return Object.entries(roman).reduce((result, [key, value]) => {
			result += key.repeat(Math.floor(year / value));
			year %= value;
			return result;
		}, '');
	};

	const roman = romanYear(year);
</script>

<footer class="flex py-4 text-center md:mt-10 mt-5">
	<div class="md:w-7/12 mx-auto font-semibold">
		<div class="md:text-sm mb-10">
			<a
				class="md:mx-4 mb-1 md:inline block hover:opacity-70"
				href="https://twitter.com/helmy_lh">
				Twitter
			</a>
			<a
				class="md:mx-4 mb-1 md:inline block hover:opacity-70"
				href="https://instagram.com/helmy.lh">
				Instagram
			</a>
		</div>

		<div class="text-sm font-normal text-neutral-400">
			<p>
				©      {roman}
				<a
					class="text-neutral-600 dark:text-neutral-200 hover:opacity-70"
					href="https://helmyl.com"
					rel="noopener noreferer"
					target="_blank">helmyl</a
				>
			</p>
		</div>
	</div>
</footer>
