<script lang="ts">
	import { createSortable, melt } from '$lib';

	const {
		elements: { zone, item },
	} = createSortable();

	const zoneItems = ['Svelte', 'JavaScript', 'TypeScript'];
</script>

<div class="mx-auto flex w-[18rem] max-w-full rounded-md">
	<div class="flex flex-col gap-3">
		<!-- Tags -->
		<div
			class="flex w-full place-content-center gap-1.5 rounded bg-white p-2 empty:opacity-0"
			use:melt={$zone({
				id: 'Tags',
				orientation: 'horizontal',
			})}
		>
			<span class="text-center text-magnum-700 [&:not(:last-child)]:hidden">
				No more tags.
			</span>

			{#each zoneItems as zoneItem}
				<div
					class="group flex cursor-move select-none items-center gap-3 rounded border border-transparent bg-magnum-500 p-1 text-white data-[sortable-dragging]:border-magnum-500 data-[sortable-dragging]:bg-magnum-300 data-[melt-sortable-ghost]:opacity-50 group-data-[sortable-id='Dropzone']:cursor-auto"
					use:melt={$item({ id: zoneItem })}
				>
					<span class="group-data-[sortable-dragging]:opacity-0">
						{zoneItem}
					</span>
				</div>
			{/each}
		</div>

		<!-- Dropzone -->
		<div
			class="group flex min-h-[3.5rem] w-72 flex-row flex-wrap place-content-center items-center gap-1.5 rounded border-2 border-dashed border-neutral-50 p-2 transition-all duration-1000 data-[sortable-focus]:border-solid"
			use:melt={$zone({
				id: 'Dropzone',
				orientation: 'horizontal',
				dropzone: true,
				fromZones: ['Tags'],
			})}
		>
			<span
				class="text-center group-data-[sortable-focus]:hidden [&:not(:last-child)]:hidden"
			>
				Dropzone
			</span>
		</div>
	</div>
</div>
