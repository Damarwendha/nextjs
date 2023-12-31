## My Notes
### Layout,
1. One benefit of using layouts in Next.js is that on navigation, only the page components update while the layout won't re-render. This is called partial rendering

### Static Rendering (by default),
1.  There are a couple of benefits of static rendering: Faster Websites and Improve SEO
2.  Static rendering is useful for UI with no data or data that is shared across users, such as a static blog post or a product page. It might not be a good fit for a dashboard that has personalized data that is regularly updated.

### Dynamic Rendering,
1. There are a couple of benefits of dynamic rendering: Real time data and Request time information such as cookies or url search params
2. To use dynamic rendering, use a Next.js API called unstable_noStore inside Server Components or data fetching functions. Example:
```
import { unstable_noStore as noStore } from 'next/cache';
 
export async function fetchRevenue() {
  // Add noStore() here to prevent the response from being cached.
  // This is equivalent to in fetch(..., {cache: 'no-store'}).
  noStore();
 
  // ...
}
```

### Fetch Data,
1. fetching data from the client, you will need an API layer that runs on the server to avoid exposing your database secrets to the client.(u don't need API layer if u on server component)

### Metadata,
```
## app/layout.tsx

import { Metadata } from 'next';
 
export const metadata: Metadata = {
  title: {
    template: '%s | Acme Dashboard',
    default: 'Acme Dashboard',
  },
  description: 'The official Next.js Learn Dashboard built with App Router.',
};
```
The %s in the template will be replaced with the specific page title.

Now, in your page.tsx you can add the page title:
```
/app/dashboard/invoices/page.tsx

export const metadata: Metadata = {
  title: 'Invoices', // the head will be Invoices | Acme Dashboard
};
```

### Font,
1. antialiased (tailwind) classname, benefit font terlihat smooth
2. pakai font dari nextjs, benefit font ringan saat proses rendering di client. example:
```
## app/ui/fonts.ts ##

import { Inter, Lusitana } from 'next/font/google';

// Primary Font
export const inter = Inter({ subsets: ['latin'] });

// Secondary Font
export const lusitana = Lusitana({
  subsets: ['latin'],
  weight: ['400', '700'],
});
```
## Random tut

### Revalidate page / path (make the data fresh again after doin something):
```
import { revalidatePath } from 'next/cache';
import { redirect } from 'next/navigation';

function handleSubmit(){
// ... //

revalidatePath('/dashboard/invoices');

// redirect to the page //
redirect('/dashboard/invoices');
}
```

### Search feature in next js:
```
  const searchParams = useSearchParams();

  const { replace } = useRouter();
  const pathname = usePathname();

  function handleSearch(term: string) {
    const params = new URLSearchParams(searchParams);

    if (term) params.set('query', term);
    else params.delete('query');

    replace(`${pathname}?${params}`);
  }
```

### How to trigger page not found
```
import { notFound } from 'next/navigation';

export default async function Page(
  // ...

  if (!invoice) {
   notFound();
  }
```
Untuk handle UI nya pakai file khusus bernama not-found.tsx

### Streaming (Loading Indicator),
There are two ways you implement streaming in Next.js: At the page level, with the loading.tsx file and For specific components, with <Suspense fallback;>

### Password hashing,
It's good practice to hash passwords before storing them in a database. Hashing converts a password into a fixed-length string of characters, which appears random, providing a layer of security even if the user's data is exposed.

In your seed.js file, you used a package called bcrypt to hash the user's password before storing it in the database. You will use it again later in this chapter to compare that the password entered by the user matches the one in the database. However, you will need to create a separate file for the bcrypt package. This is because bcrypt relies on Node.js APIs not available in Next.js Middleware.

### Handling Errors,
```
## error.tsx

'use client';

// This error prop came from throwen new Error() 
export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string };
  reset: () => void;
}) {
  useEffect(() => {
    // Optionally log the error to an error reporting service
    console.error(error);
  }, [error]);
 
  return (
      <button
        onClick={
          // Attempt to recover by trying to re-render the invoices route
          () => reset()
        }
        Try again
      </button>
  );
}
```
