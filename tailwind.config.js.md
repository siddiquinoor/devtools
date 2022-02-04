## TailwindCSS config

#

This configuration for bootstrap like media break point, color samples, fonts family, size and other utilities.

    const colors = require("tailwindcss/colors");
    const defaultTheme = require("tailwindcss/defaultTheme");

    module.exports = {
        purge: ["*.html"],
        darkMode: false, // or 'media' or 'class'
        theme: {
            screens: {
                sm: "576px",
                // => @media (min-width: 640px) { ... }

                md: "768px",
                // => @media (min-width: 768px) { ... }

                lg: "992px",
                // => @media (min-width: 1024px) { ... }

                xl: "1200px",
                // => @media (min-width: 1280px) { ... }

                "2xl": "1368px",
                // => @media (min-width: 1368px) { ... }
            },
            container: {
                center: true,
            },
            colors: {
                gray: {
                    dark: "#333333",
                    light: "#747A88",
                    muted: "#ddd",
                },
                success: "#1EC2CB",
                info: {
                    dark: "#797EF6",
                    light: "#8F98FF",
                },
                transparent: "transparent",
                current: "currentColor",
                black: colors.black,
                white: colors.white,
                background: "#24243C",
                ext1: "#7DD6F6",
                ext2: "#4ADEDE",
                ext3: "#1AA7EC",
            },
            fontSize: {
                xxx: ".5rem", // 8px
                xx: ".625rem", // 10 px
                xs: ".75rem", // 12
                sm: ".875rem", // 14
                tiny: ".875rem", // 14
                base: "1rem", // 16
                lg: "1.125rem", // 18
                xl: "1.25rem", // 20
                "2xl": "1.5rem", // 24
                "3xl": "1.875rem", // 30
                "4xl": "2.25rem", // 36
                "5xl": "3rem", // 48
                "6xl": "4rem", // 64
                "7xl": "5rem", // 80
            },
            extend: {
                fontFamily: {
                    urbanist: ["Urbanist", "sans-serif"],
                },
            },
        },
        variants: {
            extend: {},
        },
        plugins: [],
    };
