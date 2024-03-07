# Use Python 3.7 as a base image
FROM python:latest
# Copy contents into image
 COPY . .
# install pip dependencies from requirements file
RUN pip install --upgrade pip
RUN pip install -r requirements.txt
# Expose correct port
EXPOSE 5500
# Create an entrypoint
ENTRYPOINT ["python","app.py"]

