# Web Enumeration

## Overview

Port 80 was identified running Apache httpd 2.4.29 on Ubuntu. This section documents the manual review of the web service in a browser.

## Objectives

- Manually browse the exposed HTTP service
- Review the page content for useful information
- Determine whether the web service is a viable path for further exploitation

## Important Terminology

| Term | Definition |
|---|---|
| Static page | A web page that serves fixed content with no observed server-side processing |
| Page title | The content of a page's `<title>` element, often absent on placeholder or default pages |

## Concepts Explained

Nmap's banner grab reported that the site had no page title, suggesting the root page might not be a standard default Apache page. Manually browsing the service is the fastest way to confirm what is actually being served.

## Commands and Syntax

```text
Navigate to: http://10.114.175.118/
```

No CLI commands were used for this step; the service was reviewed directly in a browser.

## Command Breakdown

| Action | Purpose |
|---|---|
| Browse to `http://<target-ip>/` | View the root page exactly as served by Apache |

## Examples

Visiting `http://10.114.175.118/` rendered a full-page image styled as a "Brooklyn Nine-Nine" themed background, along with descriptive text explaining how the background image scales with the browser window.

## Screenshots

![Web Landing Page](../../images/web-http-landing-page.png)
*Root page of the HTTP service showing a static, Brooklyn Nine-Nine themed background image.*

## Observations

- The root page is static HTML displaying a full-page background image with accompanying descriptive text about the image's CSS behavior.
- No login forms, input fields, or application logic were observed on the root page.
- No further links or paths were visible directly on the page itself.

## Common Mistakes

- Dismissing a themed or "joke" landing page as having no value — it can still hint at usernames or in-jokes relevant to later credential guessing.
- Not checking the page source for hidden comments or metadata.

## Notes

- The Brooklyn Nine-Nine theme observed on this page is consistent with a username (`jake`) discovered later via the FTP note, suggesting the environment is themed around the show.
- No further web-specific attack path, such as directory fuzzing results, was documented during this session.

## Additional Context

> [!NOTE]
> The following is supplementary information, not derived from the lab notes.

In a broader assessment, this stage would typically continue with directory and file fuzzing (for example, `ffuf` or `gobuster`) and a review of HTTP response headers for further clues. See the [FFUF cheat sheet](../../cheatsheets/ffuf.md) for reference syntax.

## References

- [Apache HTTP Server Documentation](https://httpd.apache.org/docs/)

## Key Takeaways

- The web service, while thematically interesting, did not present an immediate technical vulnerability in this session.
- Thematic clues on the page aligned with usernames encountered later in the assessment, reinforcing the value of noting even seemingly cosmetic details.
