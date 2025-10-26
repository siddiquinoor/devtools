# Next.js Fundamental

## Create new project (if NPX already installed)

    npx create-next-app

## Folder structure

Private folder

    app/_lib

Route group with omit folder name from URL

    (auth)/register
    (auth)/login
    URL will be: /register, /login etc.

Passing params via URL

    /product/[productID]

Adding image sources under next.config.js

    images: {
        remotePatterns: [
            {
                protocol: "https",
                hostname: "picsum.photos",
                port: "",
                pathname: "",
            }
        ]
    }

## Using Lucide icons

To use Lucide icon add package (Ref: Lucide.dev)

    npm install lucide-react    // then import icon and use it

## Active link

Check path from URL and compare it with the link to add .active class

    import { usePathname } from "next/navigation"
    const pathName = usePathname();
    const isActive = pathName === link.href;

example of use:

    import Link from "next/link";
    import { usePathname } from "next/navigation";

    const navLinks = [
        { name: "Home", href: "/" },
        { name: "About", href: "/about" },
        { name: "Service", href: "/services" },
        { name: "Contact", href: "/contact" },
    ];

    <ul className="flex flex-row items-center gap-2">
        {navLinks.map((link) => {

            const isActive = pathName === link.href;

            return (
              <li key={link.name}>
                <Link href={link.href} className={`nav-link ${isActive && 'active'}`}>
                  {link.name}
                </Link>
              </li>
            );
        })}
    </ul>

