#CMD ["sleep", "1000"]
FROM python:3.9
EXPOSE 8080
WORKDIR /opt/server
# Runtime dependencies only
RUN apk add --no-cache pcre
# Create app user
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
USER roboshop
# Copy installed Python packages from builder
COPY --from=builder /install /usr/local
# Copy application code
COPY --chown=roboshop:roboshop payment.ini .
COPY --chown=roboshop:roboshop *.py .
CMD ["uwsgi", "--ini", "payment.ini"]