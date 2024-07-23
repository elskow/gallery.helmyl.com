<script>
	const avatar = 'https://avatars.githubusercontent.com/u/1024025?v=4';

	const username = 'helmyl';
	const uriFollow = 'https://github.com/elskow';
	const uriMessage = 'mailto:helmyl.work@gmail.com';
	const uriWebsite = 'https://helmyl.com';

	const fullName = 'Helmy Luqmanulhakim';
	const bio = 'Software engineering and Data Development.';

	export let numberPosts = 0;
</script>

<div class="flex flex-warp">
	<div class="lg:w-4/12 w-3/12 md:py-10 ml-3 md:ml-0 lg:px-20 md:px-10">
		<img
			alt="elskow"
			class="w-full rounded-full mx-auto border bg-neutral-100 border-gray-200 p-1 dark:border-neutral-800 dark:bg-black"
			height="250"
			src={avatar}
			width="250"
		/>
	</div>
	<div class="lg:w-9/12 md:w-10/12 mb-5 md:p-5 ml-5">
		<div class="md:flex items-center">
			<h2 class="text-2xl font-semibold">
				{username}
			</h2>
			<div class="md:ml-4 my-4">
				<a
					class="rounded-md bg-gray-100 px-5 font-semibold py-2 md:ml-2 text-sm leading-relaxed dark:bg-neutral-800 hover:opacity-70"
					href={uriFollow}
				>
					Follow
				</a>

				<a
					class="rounded-md bg-gray-100 px-5 font-semibold py-2 ml-2 text-sm leading-relaxed dark:bg-neutral-800 hover:opacity-70"
					href={uriMessage}
				>
					Message
				</a>
			</div>
		</div>

		<div class="md:my-5 my-3 font-bold text-sm">
			<p>{numberPosts} posts</p>
		</div>
		<p class="font-bold mb-1">
			{fullName}
		</p>
		<p>
			{bio}
		</p>

		<p class="leading-loose font-semibold text-blue-900 dark:text-blue-200">
			<a
				class="hover:underline"
				href={uriWebsite}
				rel="noopener noreferer"
				target="_blank"
			>
				{uriWebsite}
			</a>
		</p>
	</div>
</div>