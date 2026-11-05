# Relaticle on Openship (CloudShift)

Deploy config for [Relaticle](https://github.com/relaticle/relaticle), the open-source CRM, on the CloudShift HP Mini Elite through Openship. Public URL: https://aicrm.app.cloudshiftsolutions.in (the CRM itself is under `/app`).

- `docker-compose.yml`: Relaticle's own topology (app, horizon, scheduler, reverb, PostgreSQL, Redis) using the published image, pinned to a release.
- Secrets (`APP_KEY`, `DB_PASSWORD`) and `APP_URL` are set on the Openship services. Nothing secret is in this repo.

## Upgrading

Change the image tag in all four Relaticle services (`app`, `horizon`, `scheduler`, `reverb`) to the new release, push, and redeploy in Openship. Migrations run automatically when `app` starts.

## Sign-up

Relaticle's login page always offers sign-up. Email verification stays required and outgoing mail is off (`MAIL_MAILER=log`), so accounts nobody invited cannot get past "verify your email". Team members invited to a workspace are verified when they accept. To send real mail (password resets, invitations), set the `MAIL_*` variables on the services; anyone could then verify a self-made account, so consider that before enabling it.

## Admin user

```sh
docker exec -it openship-relaticle-app php artisan make:filament-user
```
